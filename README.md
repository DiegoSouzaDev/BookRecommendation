# # Zenjob - Book Recommendation Task

This is a brief proposal to solve the Book recommendation challenge, to the interview process for the Backend Engineer role.

#### Received description of the challenge
The goal of this challenge is to show how you approach a new task, interpret requirements, fill their gaps and provide a suitable solution. 
Furthermore, we want to see your understanding of basic REST APIs and how you write your code. After you finish your challenge we want to review it together with you.
When you select your tools for solving the challenge, keep in mind that on the position you applied for, we currently use mainly Groovy. 
Therefore we recommend you to use either Groovy, Java or a similar JVM language. If you don't know which framework could be suitable, consider the latest version of Grails.

#### Task:
Provide a simple book recommendation service which is usable via a REST API. 
It needs to be possible to define a new user, who will then be provided with 20 book recommendations. 
For a recommendation of a user feedback can be provided. 
The feedback can either be "liked the book", "disliked the book" or "not interested".
Requirements:
Users are identified by their username.
The list of recommendations should contain exactly 20 entries if possible.
The code should be tested as appropriated.
A suitable dataset for the books is findable alongside this challenge. 

#### Understanding:
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
`JAVA 8` -- `Spring boot` -- `MAVEN`
`Clean Architecture`

**Entity:**
User -- Book -- Recommendation

**Controller:**
`UserRestController`
| HttpMethod | Method | Description |
|------------|--------|-------------|
| `POST` | create |  Receives a `string` username and create a user, if it does not exist. |
| `GET` | getAll | Returns a Username list containing all the existing users in the application.

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


