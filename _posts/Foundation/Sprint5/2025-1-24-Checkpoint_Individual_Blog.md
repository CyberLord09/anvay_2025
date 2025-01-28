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
votes = Vote.query.filter_by(_post_id=post_id).all()
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
The `initializeSections` function illustrates these concepts:

```javascript
const voteData = await fetchVoteData();
for (const section of document.querySelectorAll("section")) {
    const sectionId = section.id;
    const isUpvoted = voteData.upvotes.includes(parseInt(sectionId));
    toggleSectionVisibility(sectionId, !isUpvoted);
}
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
return jsonify({ "message": "Vote removed" })
```

**Explanation:**
- The backend validates input parameters and returns descriptive messages or data in JSON format.

### Changing Data and Triggering Responses
Both normal and error conditions are handled effectively:

```javascript
if (!response.ok) throw new Error("Vote submission failed");
```

**Explanation:**
- The frontend checks the response status and triggers error handling when necessary.
- This approach ensures a robust user experience.

---

## Conclusion
Through careful planning and implementation, I fulfilled all project requirements by leveraging API development, frontend integration, and database management. The result is a feature-rich program that is both functional and user-friendly.

---