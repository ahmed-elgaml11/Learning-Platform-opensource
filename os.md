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
| `Post`   | `/api/v1/roadmaps/:roadmapId/courses/:courseId/topics/:topicId/completion` | Mark a topic as completed by a user    | `201 Created`                       |
| `GET`    | `/api/v1/roadmaps/:roadmapId/courses/:courseId/completion`                 | Get completed topics for a course   | `200 OK`                            |
| `GET`    | `/api/v1/roadmaps/:roadmapId/courses/:courseId/completion/progress` | To provide insights (completion percentage for a course) | `200 OK`                            |
| `DELETE` | `/api/v1/roadmaps/:roadmapId/courses/:courseId/topics/:topicId/completion` | Unmark a topic as completed            | `204 No Content` |


___

### DataBase queries and responses body
### ✅ `POST` — Mark Topic as Completed
<details>
<summary>Query</summary>


``` js
const { courseId, topicId } = req.params;
const userId = req.user.id;

  await prisma.UserCompletion.create({
    data: {
      userId,
      topicId,
      completedAt: Date.now(),
    },
  });

and basic query to get the the topicTitle

```

</details>


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
<summary>Query</summary>


``` js
const courseId = req.params.courseId
const userId = req.user.id

const completedTopics = await prisma.UserCompletion.findMany({
  where: {
    userId,
    topic: {
      courseId,
    },
  },
  include: {
    topic: true,
  },
});

```

</details>

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























### ✅ `GET` — Check Course Completion Status (completion percentage for a course)

<details>
<summary>Query</summary>


``` js
const courseId = req.params.courseId
const userId = req.user.id

const totalTopics = await prisma.Topic.findMany({
  where: {
    courseId,
  },
});

const completedTopics = await prisma.UserCompletion.findMany({
  where: {
    userId,
    topic: {
      courseId,
    },
  },
  include: {
    topic: true,
  },
});

const percent = (completedTopics.length / totalTopics.length) * 100;

```

</details>



<details>
<summary>Response Body</summary>


``` json
{
  "percentage of completion": '',
}
```

</details>





















### ✅ `DELETE` — Unmark a topic as completed



<details>
<summary>Query</summary>


``` js
const topicId = req.params.topicId
const userId = req.user.id
await prisma.UserCompletion.deleteOne({
    where: {
      userId,
      topicId
    }
})

```

</details>
























## Basic Operations:

used to get all topics
`  /api/v1/roadmaps/:roadmapId/courses/:courseId/topics
`
<details>
<summary>Query</summary>

  ``` js
const courseId = req.params.courseId
const userId = req.user.id
const topics = await prisma.Topic.findMany({
    where: {
      courseId
    }
})
```
</details>






___
used to get specific topic 
`/api/v1/roadmaps/:roadmapId/courses/:courseId/topics/:topicId `        


<details>
<summary>Query</summary>

  ``` js
const topicId = req.params.topicId
const userId = req.user.id
const topics = await prisma.Topic.findMany({
    where: {
      id: topicId
    }
})
```


</details>
























