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
    - [Distributing Information](04-Distributing-Information)
 
- #### Week 2
    - [Networking Overview](05-Networking-Overview)
    - [Layout Essentials](06-Layout-Essentials)
    - [Intro to persistence](07-Persistence)
 
- #### Week 3
    - [Generics - Functions, Protocols & Enums](08-Generics)
    - [Working with AVFoundation - Playing videos](09-Working-with-AVFoundation-Playing-Videos)

- #### Week 4
    - [Working with AVFoundation - Recording Videos](10-Working-with-AVFoundation-Recording-Videos)
    - [Persistence - Intro to Core Data](11-Persistence-Into-to-Core-Data)
    
- #### Week 5
    - Project completion/ wrap-up
 
 ## API Endpoints

| Resource                         | Endpoint                                                                     | Get URL Parameters      | Post Body                                                   | Post Body Type | Needs Authorization Header |
|----------------------------------|------------------------------------------------------------------------------|-------------------------|-------------------------------------------------------------|----------------|----------------------------|
| User                             | https://whale2-elixir.herokuapp.com/api/v1/users                             |                         |                                                             | JSON           |                            |
| Session (Current logged in user) | https://whale2-elixir.herokuapp.com/api/v1/sessions                          |                         |                                                             |                | True                       |
|                                  | https://whale2-elixir.herokuapp.com/api/v1/answers                           | per_page: Int page: Int |                                                             |                | True                       |
| Question                         | https://whale2-elixir.herokuapp.com/api/v1/questions                         | per_page: Int page: Int | receiver_id: Int  content: String                           | JSON           | True                       |
| Answer a Question                | https://whale2-elixir.herokuapp.com/api/v1/questions/**question_id**/answers |                         | video: Video File(.mov)  thumbnail: Image File(.jpeg, .png) | Multipart      | True                       |
| (Answer) Comment                 | https://whale2-elixir.herokuapp.com/api/v1/answers/**answer_id**/comments    | per_page: Int page: Int | comment: String                                             | JSON           | True                       |
| (Answer) Like                    | https://whale2-elixir.herokuapp.com/api/v1/answers/**answer_id**/likes       | per_page: Int page: Int |                                                             | JSON           | True                       |


## Sample PAW & Postman files
#### Paw File - [Link](Whale.paw)

#### Postman File [Link](Whale.postman_collection.json)