---
layout: post
title: Sprint 5 Personal Blog
description: Sprint 5 Personal Blog
type: issues
comments: True
---

### Purpose of My Group's Program
Prism is a "A platform that evolves around your connections and creativity." It's next-generation social media platform where users create customizable "Worlds" to represent their identities, collaborate with others, and connect through shared experiences. Powered by AI and enhanced with interactive storytelling, adaptive aesthetics, and emotional insights, Prism redefines how people interact online by prioritizing creativity, personalization, and meaningful connections.


### Purpose of My Individual Features
The purpose of my individual feature was to create a voting system that allows users to upvote or downvote certain things that they want appearing on thier feed. My work included implementing backend API endpoints, integrating frontend functionality, and ensuring a communication between the database and user interface.

---

## Input/Output Requests (DEMO)
Input and output functionality is essential for this project. Below, I show how these requirements were fulfilled with code examples and explanations.

### Frontend API Requests and Responses
The frontend interacts with the backend using the `fetch` API. For example, the `fetchVoteData` function retrieves vote data dynamically:

```javascript
async function fetchVoteData() {
    try {
        const voteData = { upvotes: [], downvotes: [] };
        const postIds = [1, 2, 3];

        for (const postId of postIds) {
            const response = await fetch(`${pythonURI}/api/vote/post?post_id=${postId}`, fetchOptions);
            if (!response.ok) throw new Error(`Failed to fetch votes for post ID ${postId}`);

            const data = await response.json();
            data.upvotes.forEach(vote => voteData.upvotes.push(parseInt(vote.post_id, 10)));
            data.downvotes.forEach(vote => voteData.downvotes.push(parseInt(vote.post_id, 10)));
        }

        return voteData;
    } catch (error) {
        console.error("Error fetching vote data:", error);
        return { upvotes: [], downvotes: [] };
    }
}
```

**Explanation:**
- The `fetchVoteData` function loops through an array of post IDs, making API calls for each post.
- The backend API returns JSON responses containing upvotes and downvotes, which are stored in lists (`voteData.upvotes` and `voteData.downvotes`).
- This fulfills the input/output requirement by fetching data dynamically and preparing it for further use in the application.

### Using Postman for API Testing
Here is an example of testing the `POST /vote` endpoint using Postman:

- **Request:**
  ```json
  {
      "post_id": 5,
      "vote_type": "upvote"
  }
  ```

- **Response:**
  ```json
  {
      "id": 10,
      "vote_type": "upvote",
      "user_id": 1,
      "post_id": 5
  }
  ```

**Explanation:**
- The request sends a vote type (`upvote` or `downvote`) and a post ID.
- The response confirms the vote was successfully recorded, returning the vote ID and associated details.
- Postman testing ensures the API behaves as expected and handles edge cases.


Error Codes:

![alt text]({{site.baseurl}}/images/image.png)

![alt text]({{site.baseurl}}/images/image-1.png)

### Database Initialization, Backup, and Restore
The backend provides functionality for initializing and restoring database states. For example, the `initVotes` function creates initial records:

```python
def initVotes():
    with app.app_context():
        db.create_all()
        votes = [
            Vote(vote_type='upvote', user_id=1, post_id=5),
            Vote(vote_type='downvote', user_id=2, post_id=5),
        ]
        for vote in votes:
            try:
                db.session.add(vote)
                db.session.commit()
            except IntegrityError:
                db.session.rollback()
```

**Explanation:**
- This function initializes the database schema and populates it with test data.
- In case of duplicate entries, the `IntegrityError` is caught, and the transaction is rolled back.
- These capabilities allow for efficient testing, recovery, and backup of data.


```python
    @staticmethod
    def restore(data):
        restored_classes = {}
        for vote_data in data:
            vote = Vote(vote_data['vote_type'], vote_data['user_id'], vote_data['post_id'])
            vote.create()
            restored_classes[vote_data['id']] = vote
            
        return restored_classes
```

**Explanation:**
- Restore votes from a list of dictionaries.
- data (list): List of dictionaries containing vote data.
- list: List of restored Vote objects.


---

## Working with Lists and Dictionaries

### Using Lists and Dictionaries
My project extensively uses lists and dictionaries. For instance, `fetchLeaderboard` processes data into a dictionary:

```javascript
const interestCounts = {};
allUsers.forEach(user => {
    user.interests.split(", ").forEach(interest => {
        interestCounts[interest] = (interestCounts[interest] || 0) + 1;
    });
});
```

**Explanation:**
- User interests are split into an array and tallied in the `interestCounts` dictionary.
- This structure allows for easy sorting and leaderboard generation, which improves scalability and performance.

### Querying Python Lists (Rows)
Database queries return Python lists for further processing. For example:

```python
            # Get post_id from query parameters
            post_id = request.args.get('post_id')
            
            if not post_id:
                return {'message': 'Post ID is required as a query parameter'}, 400

            # Get all votes for the post
            votes = Vote.query.filter_by(_post_id=post_id).all()
            upvotes = [vote.read() for vote in votes if vote._vote_type == 'upvote']
            downvotes = [vote.read() for vote in votes if vote._vote_type == 'downvote']

```

**Explanation:**
- The `filter_by` method, provided by SQLAlchemy (a 3rd-party library), retrieves all votes associated with a specific post ID.
- This results in a list of `Vote` objects that can be further manipulated or converted into JSON format for API responses.

### Mapping Rows to JSON Responses
The `read` method in the `Vote` class converts the database rows into a JSON-compatible dictionary:

```python
def read(self):
    return {
        "id": self.id,
        "vote_type": self._vote_type,
        "user_id": self._user_id,
        "post_id": self._post_id
    }
```

**Explanation:**
- This ensures seamless integration of database data into API responses.
- The use of SQLAlchemy simplifies the querying process while maintaining scalability.

---

## Formatting API Responses into the DOM

The `fetchSuggestions` function demonstrates this process:

```javascript
matchedUsers.forEach(user => {
    const card = document.createElement("div");
    card.className = "profile-card";
    card.textContent = `${user.name} - Interests: ${user.interests}`;
    suggestionsContainer.appendChild(card);
});
```

**Explanation:**
- The function loops through the list of matched users, creating DOM elements dynamically.
- Each user's data is displayed as a styled card in the UI.
- This approach ensures the frontend remains responsive and user-friendly.

---

## API Methods and Algorithmic Code

### CRUD Operations in the API
The `VoteAPI` class handles all CRUD operations. For example:

```python
class _CRUD(Resource):
    @token_required()
    def post(self):
        data = request.get_json()
        vote = Vote(data['vote_type'], current_user.id, data['post_id'])
        vote.create()
        return jsonify(vote.read())
```

**Explanation:**
- The `post` method extracts data from the request body, creates a `Vote` object, and saves it to the database.
- The `token_required` decorator ensures only authenticated users can access this endpoint.

### Sequencing, Selection, and Iteration
The `get` function illustrates these concepts:

```python
    class _POST_VOTES(Resource):
            # Get all votes for the post
            votes = Vote.query.filter_by(_post_id=post_id).all()
            upvotes = [vote.read() for vote in votes if vote._vote_type == 'upvote']
            downvotes = [vote.read() for vote in votes if vote._vote_type == 'downvote']

            result = {
                "post_id": post_id,
                "upvote_count": len(upvotes),
                "downvote_count": len(downvotes),
                "total_votes": len(votes),
                "upvotes": upvotes,
                "downvotes": downvotes
            }
            return jsonify(result)
```

**Explanation:**
- The function sequences calls to fetch data, process it, and update the DOM.
- It uses conditional logic (`if`) to determine visibility for each section.
- Iteration ensures all sections are processed efficiently.

---

## Handling Data and Responses

### Parameters and Return Types
Endpoints use parameters like `post_id` and `vote_type`, returning JSON responses:

```python
            result = {
                "post_id": post_id,
                "upvote_count": len(upvotes),
                "downvote_count": len(downvotes),
                "total_votes": len(votes),
                "upvotes": upvotes,
                "downvotes": downvotes
            }
            return jsonify(result)
```

**Explanation:**
- The backend validates input parameters and returns descriptive messages or data in JSON format.

### Changing Data and Triggering Responses
Both normal and error conditions are handled effectively:

```javascript

            # Validate required fields
            if not data:
                return {'message': 'No input data provided'}, 400
            if 'post_id' not in data:
                return {'message': 'Post ID is required'}, 400
            if 'vote_type' not in data or data['vote_type'] not in ['upvote', 'downvote']:
                return {'message': 'Vote type must be "upvote" or "downvote"'}, 400

                
if (!response.ok) throw new Error("Vote submission failed");
```

**Explanation:**
- The frontend checks the response status and triggers error handling when necessary.
- This approach ensures a robust user experience.

---

## Conclusion
Through careful planning and implementation, I fulfilled all project requirements by leveraging API development, frontend integration, and database management. The result is a feature-rich program that is both functional and user-friendly.

---



## Key Concepts

-   Computer systems consist of hardware, software, and data that work together to perform specific tasks and solve problems
-   Networks enable computer systems to communicate and share resources (data, devices, services) with each other
-   Data transmission involves sending digital data over a communication channel from a sender to a receiver
-   Protocols are sets of rules that govern how devices communicate and exchange data over a network
-   Network security measures protect computer systems and data from unauthorized access, use, disclosure, disruption, modification, or destruction
-   Troubleshooting is the systematic process of identifying, diagnosing, and resolving problems in computer systems and networks
    -   Involves gathering information, analyzing symptoms, identifying potential causes, and implementing solutions
-   Computer systems and networks have numerous real-world applications across various industries (healthcare, education, finance, entertainment)

## System Components

-   Hardware refers to the physical components of a computer system that can be touched (motherboard, CPU, RAM, storage devices)
-   Software is a set of instructions that tells the hardware what to do and how to perform specific tasks
    -   Includes operating systems (Windows, macOS, Linux), applications, and utilities
-   Data is the information processed, stored, and transmitted by computer systems
    -   Can be in various forms such as text, numbers, images, audio, and video
-   Input devices allow users to enter data and commands into a computer system (keyboard, mouse, touchscreen, microphone)
-   Output devices present information to users from a computer system (monitor, printer, speakers)
-   Processing devices perform computations and execute instructions (CPU, GPU)
-   Storage devices retain data and programs for future use (hard disk drives, solid-state drives, USB flash drives, optical discs)

## Network Fundamentals

-   A network is a group of interconnected devices that can communicate and share resources with each other
-   Network topology refers to the arrangement and layout of devices and connections in a network
    -   Common topologies include bus, star, ring, mesh, and tree
-   Network types can be classified based on size, geographical coverage, and ownership
    -   Local Area Network (LAN) covers a small area (home, office, school)
    -   Wide Area Network (WAN) spans a large geographical area (cities, countries, continents)
-   Network devices facilitate communication and data transfer between connected devices
    -   Switches connect devices within a network and forward data packets to the intended destination
    -   Routers connect multiple networks and determine the best path for data packets to reach their destination
-   Network media refers to the physical channels used to transmit data between devices
    -   Wired media includes coaxial cables, twisted pair cables, and fiber optic cables
    -   Wireless media uses radio waves to transmit data (Wi-Fi, Bluetooth, cellular networks)

## Data Transmission

-   Data transmission is the process of sending digital data from one device to another over a communication channel
-   Bandwidth refers to the maximum amount of data that can be transmitted over a channel in a given period of time
    -   Measured in bits per second (bps), kilobits per second (Kbps), megabits per second (Mbps), or gigabits per second (Gbps)
-   Latency is the time delay between the sender transmitting data and the receiver receiving it
    -   Measured in milliseconds (ms) or seconds (s)
-   Packet switching is a method of transmitting data over a network by breaking it into smaller units called packets
    -   Each packet contains a source address, destination address, and a portion of the data being sent
-   Circuit switching is a method of transmitting data over a network by establishing a dedicated communication channel between the sender and receiver
    -   Commonly used in traditional telephone networks
-   Multiplexing techniques allow multiple signals or data streams to be combined and transmitted over a single communication channel
    -   Time-division multiplexing (TDM) allocates time slots to each data stream
    -   Frequency-division multiplexing (FDM) assigns different frequency bands to each data stream

## Protocols and Standards

-   Protocols are sets of rules and conventions that govern how devices communicate and exchange data over a network
-   The Open Systems Interconnection (OSI) model is a conceptual framework that standardizes communication functions in a network
    -   Consists of seven layers: Physical, Data Link, Network, Transport, Session, Presentation, and Application
-   The Transmission Control Protocol/Internet Protocol (TCP/IP) is a suite of protocols used in computer networks and the Internet
    -   Consists of four layers: Network Access, Internet, Transport, and Application
-   Hypertext Transfer Protocol (HTTP) is an application-layer protocol used for transmitting web pages and other content over the Internet
-   File Transfer Protocol (FTP) is an application-layer protocol used for transferring files between computers over a network
-   Simple Mail Transfer Protocol (SMTP) is an application-layer protocol used for sending and receiving email messages
-   Domain Name System (DNS) is a hierarchical naming system that translates human-readable domain names into IP addresses
-   Standards organizations develop and maintain protocols and standards to ensure interoperability between devices and networks
    -   Examples include the Internet Engineering Task Force (IETF), Institute of Electrical and Electronics Engineers (IEEE), and International Organization for Standardization (ISO)

## Security and Privacy

-   Network security involves protecting computer systems, networks, and data from unauthorized access, use, disclosure, disruption, modification, or destruction
-   Confidentiality ensures that data is accessible only to authorized users and is protected from unauthorized disclosure
    -   Achieved through encryption, access controls, and secure communication channels
-   Integrity ensures that data remains accurate, complete, and unaltered during transmission and storage
    -   Achieved through error detection and correction, digital signatures, and hashing algorithms
-   Availability ensures that data and resources are accessible to authorized users when needed
    -   Achieved through redundancy, backup systems, and disaster recovery plans
-   Authentication is the process of verifying the identity of a user or device before granting access to resources
    -   Achieved through usernames and passwords, biometric data, digital certificates, and multi-factor authentication
-   Authorization is the process of granting or denying access to resources based on a user's authenticated identity and permissions
    -   Achieved through access control lists (ACLs), role-based access control (RBAC), and attribute-based access control (ABAC)
-   Firewalls are security devices that monitor and control incoming and outgoing network traffic based on predetermined security rules
    -   Can be hardware-based or software-based
-   Virtual Private Networks (VPNs) create secure, encrypted connections over public networks (Internet) to protect data privacy and integrity

## Troubleshooting and Maintenance

-   Troubleshooting is the systematic process of identifying, diagnosing, and resolving problems in computer systems and networks
-   The first step in troubleshooting is to gather information about the problem, including symptoms, error messages, and any recent changes to the system
-   Next, analyze the information collected to identify potential causes of the problem
    -   Use a process of elimination to narrow down the list of possible causes
-   Once the root cause is identified, implement a solution to resolve the problem
    -   This may involve updating software, replacing hardware components, or modifying configuration settings
-   After implementing the solution, test the system to ensure that the problem has been resolved and no new issues have been introduced
-   Document the troubleshooting process, including the problem description, steps taken, and the resolution for future reference
-   Preventive maintenance involves regularly scheduled tasks to keep computer systems and networks running smoothly and prevent potential problems
    -   Includes updating software, cleaning hardware components, and performing data backups
-   Monitoring tools and techniques help detect and diagnose problems before they cause significant disruptions
    -   Examples include network monitoring software, system logs, and performance metrics

## Real-World Applications

-   Healthcare: Computer systems and networks enable electronic health records (EHRs), telemedicine, and medical imaging
    -   Facilitates efficient patient care, improves diagnostic accuracy, and enhances collaboration among healthcare providers
-   Education: Computer systems and networks support online learning platforms, educational resources, and collaborative tools
    -   Enables distance learning, personalized instruction, and access to a wide range of educational materials
-   Finance: Computer systems and networks are critical for electronic trading, online banking, and secure financial transactions
    -   Ensures fast, reliable, and secure processing of financial data and reduces the risk of fraud and errors
-   Entertainment: Computer systems and networks power streaming services (Netflix, Spotify), online gaming, and social media platforms
    -   Provides users with on-demand access to a vast library of content and enables interactive experiences and social connections
-   Transportation: Computer systems and networks enable intelligent transportation systems, GPS navigation, and autonomous vehicles
    -   Improves traffic management, enhances safety, and optimizes route planning and logistics
-   Manufacturing: Computer systems and networks support computer-aided design (CAD), computer-aided manufacturing (CAM), and industrial automation
    -   Increases production efficiency, reduces costs, and improves product quality and consistency
-   E-commerce: Computer systems and networks are the backbone of online marketplaces (Amazon, eBay) and digital payment systems
    -   Enables businesses to reach a global customer base, streamlines transactions, and facilitates secure online payments