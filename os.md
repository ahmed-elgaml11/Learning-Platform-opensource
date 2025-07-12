###  one of the main steps to system design a feature is to reduce the feature into data definition 


#### Feature: 

   Allow the user to mark content as completed after finishing it.

#### data definition: 

consept of somebody completing some topic which can be an object with id, title, content, expected duration
and finally we can map it into db. 
___


### once of defining the data we should define endpoints:







| Method   | Endpoint                                                                               | Description                            | Response status                     |
| -------- | -------------------------------------------------------------------------------------- | -------------------------------------- | ----------------------------------- |
| `POST`   | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Mark a topic as completed by a user    | `201 Created`                       |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/completion`                 | Get completed topic IDs for a course   | `200 OK`                            |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Check if a specific topic is completed | `200 OK`                            |
| `DELETE` | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Unmark a topic as completed            | `204 No Content` |


### ✅ `POST` — Mark Topic as Completed

<details>
<summary>Response Body</summary>


``` json
{
  "message": "Topic marked as completed",
  "data": {
    "userId": "",
    "topicId": "",
    "topicTitle": "",
    "courseId": "",
    "completedAt": ""
  }
}
```

</details>




### ✅ `GET` — Get Completed Topics in a Course

<details>
<summary>Response Body</summary>


``` json
{
  "courseId": "",
  "completedTopics": [
    { "topicId": "", "completedAt": "" },
    { "topicId": "", "completedAt": "" }
  ]
}
```

</details>






### ✅ `GET` — Check Topic Completion Status

<details>
<summary>Response Body</summary>


``` json
{
  "completed": true,
  "completedAt": "2025-07-12T01:30:00Z"
}
or
{
  "completed": false
}

```

</details>




</details>
