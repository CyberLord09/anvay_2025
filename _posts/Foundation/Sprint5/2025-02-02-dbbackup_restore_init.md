---
layout: post
title: Utilization of DB Scripts
description: Understanding db_init, db_backup, and db_restore while creating a backup and restore sequence.
type: issues
comments: True
---

# **Automating Database Backups with Cron**

### **Introduction**
Database integrity is crucial for any application, and ensuring that backups are automatically created can prevent data loss in case of unexpected failures. In this tutorial, I’ll walk through how I set up a **cron job** that automates database backups for my **Prism Backend**, ensuring that even if data is wiped, we can quickly restore it.

---

## **Setting Up the Backup Sequence**
To automate the backup process, I created a **Bash script** that:
1. Navigates to the backend project directory.
2. Activates a Python virtual environment.
3. Installs necessary dependencies.
4. Runs the **backup script** to save the database.

### **Bash Script: `prism_backup_sequence.sh`**
```bash
#!/bin/bash

cd /home/ubuntu/prism_backend

# Verify the installation and check the Python version
python --version

# Create a virtual environment if it doesn't exist
if [ ! -d "venv" ]; then
    python -m venv venv
fi

# Activate the virtual environment
source venv/bin/activate

# Install the required Python packages
pip install -r requirements.txt

# Run the database backup script
cd /home/ubuntu/prism_backend
./scripts/db_backup.py
```

---

## **Automating the Backup Process with Cron**
Now that we have a working backup script, we need to ensure that it runs **automatically at a scheduled time**. This is where **cron** comes in.

### **Configuring Cron**
Cron is a Unix-based job scheduler that allows us to execute commands at specified intervals. To run our backup script every day at **1:00 AM**, I added the following cron job:

```cron
0 1 * * * bash /home/ubuntu/prism_backend/scripts/prism_backup_sequence.sh
```

This cron job ensures that backups happen daily without requiring manual intervention.

---

## **The Python Backup Script (`db_backup.py`)**
Our Python script is responsible for actually performing the backup by saving the current database state into a JSON file. This allows us to restore data later if needed.

```python
#!/usr/bin/env python3

""" db_backup.py
Backs up the current database and saves the data to JSON files.

Usage: Run from the terminal as such:

Goto the scripts directory:
> cd scripts; ./db_backup.py

Or run from the root of the project:
> scripts/db_backup.py
"""

import sys
import os

# Add the directory containing main.py to the Python path
sys.path.append(os.path.abspath(os.path.join(os.path.dirname(__file__), '..')))

from main import app, backup_data

def main():
    # Step 1: Backup the old database
    with app.app_context():
        backup_data()

if __name__ == "__main__":
    main()
```

This script calls **`backup_data()`**, a function from `main.py` that handles exporting database records into JSON format. Running this script ensures that we have a **snapshot of the database** before any changes occur.

---

## **Handling Database Schema Changes Without Losing Data**
One common issue when modifying a database schema is the risk of **wiping out existing data**. To prevent this, we take the following approach whenever we introduce schema changes:

### **Ensuring Safe Schema Updates in Docker**
When the database schema is modified, we don’t want to lose any valuable data. To prevent this, we added the following steps in our **Dockerfile**:

```dockerfile
RUN ./scripts/db_backup.py  # Backup existing data
RUN ./scripts/db_init.py    # Reinitialize the database with new schema changes
RUN ./scripts/db_restore.py # Restore the backed-up data into the modified schema
```

### **Why This Works**
1. **Backup Data** → Before making any schema modifications, we save all existing data.
2. **Reinitialize the Database** → We apply the updated schema, adding new tables and columns.
3. **Restore Old Data** → The previously backed-up records are inserted back into the new schema structure, ensuring no data loss.

This approach ensures **smooth schema migrations** while keeping all user data safe.

---

## **Conclusion**
With this setup:
- **Backups are automated** via a cron job running daily.
- **Data is preserved before schema changes**, preventing accidental data loss.
- **A structured recovery process** ensures quick restoration if anything goes wrong.

