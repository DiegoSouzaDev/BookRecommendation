# Book Recommendation Task

This is a brief proposal to solve the Book recommendation challenge, to the interview process for the Backend Engineer role.

#### Understanding of the Task:
The ideal scenario would take longer then the suggested time to solve this task, so, I will describe a "basic scenario" to the solution and, in a later topic, describe how I figure the ideal scenario. 

#### Basic Solution:
The basic solution consists in the following itens:
- The data provided with the task has to be loaded to a `repository`. 
- Has to provide a way to register a `user` by a given a non-existen `username`.
- When a user is created, the system has to recommend 20 books for that user, using the given book data that was sent with the task.
- The user must be allowed to consult his list of recommendations and then give a feedback about those books, individually.
- When a feedback is registered, that recommended book is no longer a valid recommendation for the current user and a new recommendation must be made in order to keep the user with 20 valid recommendations whenever is possible.

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
| `GET` | getAll | Returns a Username list containing all the existing users in the application.|

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


