#  API Specification

##  one of the main steps to system design a feature is to reduce the feature into data definition 


### Feature: 

   Allow the user to mark content as completed after finishing it.

### data definition: 

- we have many tracks each one has many courses each one has many topics 
-  consept of somebody completing some topic which can be an object with id, title, content, expected duration
and finally we can map it into db. 

___


## once of defining the data we should define endpoints:




## 📘 Track Endpoints

### ✅ GET `/tracks`

- **Description:** Retrieves all available tracks.
- **Response:** `200 OK` with a list of tracks.

**Query Example:**
```ts
const tracks = await prisma.track.findMany();
```
**Response Body:**
``` json
{
  lenghth: tracks.length
  tracks: [
    {
      id,
      title,
      description
    }
  ]

  
}
```


### ✅ GET `/tracks/:trackId `

- **Description:** Retrieve a specific track by ID and all courses in this track.
- **Response:** `200 OK` with a single track and a list of all track courses.

**Query Example:**

```ts
const track = await prisma.track.findUnique({
  where: {
    id: req.params.trackId
  }
});

const courses = await prisma.course.findMnay({
  where: {
    trackId: req.params.trackId
  },
  orderBy: {
    order: 'asc'
  }
})
```
**Response Body:**

``` json

{
  track: [
    {
      id,
      title,
      description
    }
  ],
  courses: [
    {
      title
    }
  ]
  
}
```









## 📘 Course Endpoints


### ✅ GET `/courses/:courseId `

- **Description:** Retrieve a specific Course by ID and all topics in this course and completion percentage for a course .
- **Response:** `200 OK` with a single Course and alist of course topics and completion percentage for a course .
 **Query Example:**

```ts
const course = await prisma.course.findUnique({
  where: {
    id: req.params.courseId
  }
});

const totalTopics = await prisma.topic.findMnay({
  where: {
    courseId: req.params.courseId
  },
  orderBy: {
    order: 'asc'
  }
})


const completedTopics = await prisma.userCompletion.findMany({
  where: {
    userId: req.user.id,
    topic: {
      courseId: req.params.courseId
    }

  },
  select: {
    topic: true
  }

})
const persentage = (completedTopics.length/ totalTopics.length) * 100
```

**Response Body:**
``` json 
  course:{
    title, 
    description
  },
  totalToics: {
    title
  },
  persentage

```





### ✅ GET `/courses/:courseId/topics `

- **Description:** get completed and uncompleted topics in the course .
- **Response:** `200 OK` with a single Course and alist of course topics and completion percentage for a course .
- **Query Example:**

```ts

const totalTopics = await prisma.topic.findMnay({
  where: {
    courseId: req.params.courseId
  },
  orderBy: {
    order: 'asc'
  }
})

const completedTopics = await prisma.userCompletion.findMany({
  where: {
    userId: req.user.id,
    topic: {
      courseId: req.params.courseId
    }

  },
  select: {
    topic: true
  }
})

const completedTopicsIds = completedTopics.map(ele => ele.topic.id)
const unCompletedTopics = await totalTopics.filter(ele => !completedTopicsIds.includes(ele.id) )


```

**Response Body:**
``` json 
  completedTopics:{
    title, 
    description,
    duration
  },
  completedTopicsIds: {
    title, 
    description,
    duration
  },

```











## 📘 Topic Endpoints



### ✅ GET `/topics/:topicId `

- **Description:** Retrieve a specific topic by ID .
- **Response:** `200 OK` with a single topic.
**Query Example:**

```ts
const topic = await prisma.topic.findUnique({
  where: {
    id: req.params.topicId
  }
});
```

**Response Body:**
``` json 
topic: {
  title,
  duration,
  content
}
```



### ✅ Post `/topics/:topicId/completion` 

- **Description:** Mark a topic as completed by a user .
- **Response:** `201 Created` with the completed topic.
**Query Example:**

```ts
const topic = await prisma.userCompleteion.create({
  data: {
    userId: req.user.id,
    topicId: req.params.topicId
  }
});
```
**Response Body:**
``` json 
topic: {
  title,
  duration,
  content
}
```




### ✅ Delete `/topics/:topicId/completion` 

- **Description:** Unmark a topic as completed .
- **Response:** ` 204 No Content`.
**Query Example:**

```ts
const topic = await prisma.userCompleteion.delete({
  where: {
    userId: req.user.id,
    topicId: req.params.topicId
  }
});
```
