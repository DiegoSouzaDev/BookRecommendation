# Book Recommendation Task

This is a brief proposal to solve the Book recommendation challenge, to the interview process for the Backend Engineer role.

#### Understanding of the Task:
My understanding of the challenge, is that it asks for an api to simulate a store showcase with 20 books that has never got a feedback for that user.
The ideal scenario would take longer then the suggested time to solve this task, so, I will describe a "basic scenario" to the solution and, in a later topic, describe how I figure the ideal scenario. 

#### Basic Solution:
Lets consider that the window shown to the user is dinamic, and will change every time he visits the page, as is common in the e-commerces, and  that once the user send a feedback to a book, that book will no longer be displayed as a recommendation.

The basic solution consists in the following itens:
- The data provided with the task has to be loaded to a `repository`. 
- Has to provide a way to register a `user` by a given a non-existen `username`.
- When a user consult the list of recommendations, the system has to recommend 20 books for that user, using the given book data that was sent with the task.
- The user must be allowed give a feedback about those recommended books, individually.
- When a feedback is registered, that recommended book is no longer a valid recommendation for the current user and should not be recommended again to this user.
- when a feedback is sent by the user, the system must keep record of the nature of that feedback and consider this in the next recommendation to the user.

##### Technical description for the basic solution:
**Project**
`JAVA 8` -- `Spring boot` -- `MAVEN` -- `JUnit`
`Clean Architecture`

**Entity:**
User -- Book -- Recommendation

**Controller:**
`UserRestController`

| HttpMethod | Method | Description |
|------------|--------|-------------|
| `POST` | create |  Receives a `string` username and create a user, if it does not exist. |


`RecommendationRestController`

| HttpMethod | Method | Description |
|------------|--------|-------------|
|`GET`|getByUserName|Return all the **valid** recommendations for given `username`. By valid, are all the recommendations that doesnt have a feedback.|

`FeedBackRestController`

| HttpMethod | Method | Description |
|------------|--------|-------------|
|`POST`|create|Receives the `recommendationId` and a `int` parameter (`-1`, `0`, `1`) representing a negative, neutral or positive feedback. This parameter will be used to update the recommendation and by that, generate a new recommendation to the received username|

**Usecase:**
`RecommendationUsecase` 

|Method | Resposibility |
|-------------|-------------|
|generateStartRecommendation| Provide a new user with 20 book recommendation|
|recommendABook| Provide a new book recommendation to a user. A book can only be recommended once to the same user   |
|getAllValidRecommendation||

