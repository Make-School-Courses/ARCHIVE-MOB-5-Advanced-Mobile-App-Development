# End-To-End iOS Development

The goal of this class is to build a video Q&A app modeled after the Whale iOS App. We will focus on building only a subset of features of the Whale app, with a focus on **netwoking**, **architecture** and a bit of fun with video with **AVFoundation**. 

## Objectives

- Build an iOS app from an API specification
- Use AVFoundation to play, record and save videos & photos
- Leverage advanced Swift features to architect your app
- Build common app features like networking, authentication, pagination

## Course Outline

- #### Week 1
    - [Project Overview](01-Assigned-Project)
    - [App Architecture](02-App-architecture)
    - [Dependency Management](03-Dependency-Management)
    - [Intro to persistence](04-Intro-to-Persistence)
 
- #### Week 2
    - [Distributing Information](05-Distributing-Information)
    - [Networking Overview](06-Networking-Overview)
    - [Layout Essentials](07-Layout-Essentials)
 
- #### Week 3
    - [Generics - Functions, Protocols & Enums](08-Generics)
    - [Working with AVFoundation - Playing videos](09-Working-with-AVFoundation-Playing-Videos)

- #### Week 4
    - [Working with AVFoundation - Recording Videos](10-Working-with-AVFoundation-Recording-Videos)
    - [Persistence - Intro to Core Data](11-Persistence-Intro-to-Core-Data)
    
- #### Week 5
    - Project completion/ wrap-up
 
 ## API Endpoints

| Resource                | Endpoint                                                                     | Request Type | URL Parameters                    | Body                                                                                                            | Body Type       | Needs Authorization Header | Description                                                                                                  |
|-------------------------|------------------------------------------------------------------------------|--------------|-----------------------------------|-----------------------------------------------------------------------------------------------------------------|-----------------|----------------------------|--------------------------------------------------------------------------------------------------------------|
| Get Users               | https://whale2-elixir.herokuapp.com/api/v1/users                             | GET          | per_page: Intpage: Int            | -                                                                                                               | JSON            | False                      | Fetches all Users                                                                                            |
| Create User             | https://whale2-elixir.herokuapp.com/api/v1/users                             | POST         | -                                 | email: String first_name: String last_name: String password: String username: String image_url: Optional - File | JSON/ Multipart | False                      | Creates a User. If the image_url is passed in with a file, the profile photo of the user is uploaded as well |
| Login User              | https://whale2-elixir.herokuapp.com/api/v1/sessions                          | POST         | email: String password: String | -                                                                                                               | -               | False                      | Login a User                                                                                                 |
| Get Answers             | https://whale2-elixir.herokuapp.com/api/v1/answers                           | GET          | per_page: Intpage: Int            | -                                                                                                               | -               | True                       | Fetches all Answers                                                                                          |
| Get Answer Comments     | https://whale2-elixir.herokuapp.com/api/v1/answers/**answer_id**/comments    | GET          | per_page: Intpage: Int            | -                                                                                                               | -               | True                       | Fetches all comments for an Answer                                                                           |
| Get Answer Likes        | https://whale2-elixir.herokuapp.com/api/v1/answers/**answer_id**/likes       | GET          | per_page: Intpage: Int            | -                                                                                                               | -               | True                       | Fetches all likes for an Answer                                                                              |
| Create/Upload an Answer | https://whale2-elixir.herokuapp.com/api/v1/questions/**question_id**/answers | POST         | -                                 | video: File thumbnail: File                                                                                     | Multipart       | True                       | Creates an Answer; uploads the answer video and thumbnail                                                    |
| Get My Questions        | https://whale2-elixir.herokuapp.com/api/v1/questions                         | GET          | per_page: Intpage: Int            | -                                                                                                               | -               | True                       | Fetches all questions for a logged in User                                                                   |
| Create Question         | https://whale2-elixir.herokuapp.com/api/v1/questions                         | POST         | -                                 | receiver_id: Intcontent: String                                                                                 | JSON            | True                       | Creates a question for a User(receiver)                                                                      |


## Sample PAW & Postman files
#### Paw File - [Link](Whale.paw)

#### Postman File [Link](Whale.postman_collection.json)