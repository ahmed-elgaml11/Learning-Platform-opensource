###  one of the main steps to system design a feature is to reduce the feature into data definition 


#### Feature: 

   Allow the user to mark content as completed after finishing it.

#### data definition: 

consept of somebody completing some content which can be an object with id, num of items, timeline, userid,..
and finally we can map it into db. 
___


### once of defining the data we should define endpoints 










| Method   | Endpoint                                                                               | Description                                                 | Response Body                                                                                                                                         |
| -------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `POST`   | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Mark a topic as completed by a user                         | `201 Created`<br>`{ "message": "Topic marked as completed", "data": { "userId": "...", "topicId": "...", "courseId": "...", "completedAt": "..." } }` |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/completion`                 | Returns a list of completed topic IDs for the learner for specific course       | `200 OK`<br>`{ "courseId": "...", "completedTopics": [ { "topicId": "...", "completedAt": "..." }, ... ] }`                                           |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Get completion status (completed or not) for specific topic | `200 OK`<br>`{ "Completed": true/false, "completedAt": "..."/ null      
}`                                                      |
| `DELETE` | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Unmark a topic as completed                                 | `204 NO Content`             |
























| Method   | Endpoint                                                                               | Description                                                   | Response Body                                                                                                                                                                                                 |
| -------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `POST`   | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Mark a topic as completed by a user                           | **201 Created**<br>`json<br>{<br>  "message": "Topic marked as completed",<br>  "data": {<br>    "userId": "...",<br>    "topicId": "...",<br>    "courseId": "...",<br>    "completedAt": "..."<br>  }<br>}` |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/completion`                 | Get all completed topics for the learner within a course      | **200 OK**<br>`json<br>{<br>  "courseId": "...",<br>  "completedTopics": [<br>    { "topicId": "...", "completedAt": "..." },<br>    ...<br>  ]<br>}`                                                         |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Get completion status (completed or not) for a specific topic | **200 OK**<br>`json<br>{<br>  "completed": true,<br>  "completedAt": "..."<br>}`<br>or<br>`json<br>{<br>  "completed": false<br>}`                                                                            |
| `DELETE` | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion` | Unmark a topic as completed                                   | **204 No Content** (no response body on success)<br>or<br>**404 Not Found**<br>`json<br>{<br>  "message": "Topic was not marked as completed"<br>}`                                                           |






















| Method   | Endpoint                                                                                   | Description                                                   | Response Body |
|----------|--------------------------------------------------------------------------------------------|---------------------------------------------------------------|---------------|
| `POST`   | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion`     | Mark a topic as completed by a user                           | **201 Created**<br>```json<br>{<br>  "message": "Topic marked as completed",<br>  "data": {<br>    "userId": "...",<br>    "topicId": "...",<br>    "courseId": "...",<br>    "completedAt": "..."<br>  }<br>}``` |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/completion`                     | Get all completed topics for the learner within a course      | **200 OK**<br>```json<br>{<br>  "courseId": "...",<br>  "completedTopics": [<br>    { "topicId": "...", "completedAt": "..." },<br>    ...<br>  ]<br>}``` |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion`     | Get completion status (completed or not) for a specific topic | **200 OK**<br>```json<br>{<br>  "completed": true,<br>  "completedAt": "..."<br>}```<br>or<br>```json<br>{<br>  "completed": false<br>}``` |
| `DELETE` | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion`     | Unmark a topic as completed                                   | **204 No Content** (no response body)<br>or<br>**404 Not Found**<br>```json<br>{<br>  "message": "Topic was not marked as completed"<br>}``` |




| Method   | Endpoint                                                                                   | Description                                                   | Response Body |
|----------|--------------------------------------------------------------------------------------------|---------------------------------------------------------------|---------------|
| `POST`   | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion`     | Mark a topic as completed by a user                           | **201 Created**<br>```json\n{\n  "message": "Topic marked as completed",\n  "data": {\n    "userId": "...",\n    "topicId": "...",\n    "courseId": "...",\n    "completedAt": "..." \n  }\n}``` |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/completion`                     | Get all completed topics for the learner within a course      | **200 OK**<br>```json\n{\n  "courseId": "...",\n  "completedTopics": [\n    { "topicId": "...", "completedAt": "..." },\n    ...\n  ]\n}``` |
| `GET`    | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion`     | Get completion status (completed or not) for a specific topic | **200 OK**<br>```json\n{\n  "completed": true,\n  "completedAt": "..." \n}```<br>or<br>```json\n{\n  "completed": false \n}``` |
| `DELETE` | `/api/v1/tracks/:trackId/levels/:levelId/courses/:courseId/topics/:topicId/completion`     | Unmark a topic as completed                                   | **204 No Content**<br>or<br>**404 Not Found**<br>```json\n{\n  "message": "Topic was not marked as completed"\n}``` |
