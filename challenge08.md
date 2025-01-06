# Challenge 08 - Add/Update feedback for a movie

For this challenge you need to implement the following API endpoints

```http
POST /api/feedback
GET /api/feedback/:movieId
```

## Part a

When a user submits feedback, including a rating and comment, for a movie they haven't reviewed before, the system should save it in the feedback table.

- You need to complete `addFeedback()` function in `feedbackController` and `feedbackRepository`to implement this scenario.

The response should be similar to the following.

```json
"data": {
        "userId": "c784dd78-b26e-4cc0-9c8a-b84bdb4330b9",
        "movieId": "a742a595-e707-458a-9240-66742251dabf",
        "rating": 5,
        "comment": "Great movie! I loved it! The plot was amazing and the acting was superb!",
        "createdAt": "2024-04-15T10:36:51.658Z"
    }
```

## Part b

When a user attempts to submit additional feedback for a movie they've already reviewed, the system should update the existing feedback in the database and retrieve it.

- You need to implement the `getSingleFeedback()` function in `feedbackRepository`
- you need to modify `addFeedback()` function in `feedbackController` to implement this scenario.

The response should look like this.

```json
"data": {
        "userId": "c784dd78-b26e-4cc0-9c8a-b84bdb4330b9",
        "movieId": "b5f37e47-40a7-4688-b6aa-420356eabcf8",
        "rating": 4,
        "comment":"Interesting movie! The plot was intriguing and the acting was good! I would watch it again!",
        "createdAt": "2024-04-15T11:15:54.299Z"
    }
```


