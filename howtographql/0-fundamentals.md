# HowToGraphQL Fundamentals

## Introduction

### What is an API

`In short, an API defines how a client can load data from a server.`

### How is GraphQL different

At its core, GraphQL enables declarative data fetching where a client can specify exactly what data it needs from an API.
Instead of multiple endpoints that return fixed data structures, a GraphQL server only exposes a single endpoint and responds with precisely the data a client asked for.

GraphQL is often confused with being a database technology. This is a misconception, GraphQL is a query language for APIs - not databases. In that sense it’s database agnostic and effectively can be used in any context where an API is used.

## GraphQL is the better REST

To illustrate the major differences between REST and GraphQL when it comes to fetching data from an API, let’s consider a simple example scenario: In a blogging application, an app needs to display the titles of the posts of a specific user. The same screen also displays the names of the last 3 followers of that user. How would that situation be solved with REST and GraphQL?

### Data Fetching with REST vs GraphQL

With a REST API, you would typically gather the data by accessing multiple endpoints. In the example, these could be `/users/<id> `endpoint to fetch the initial user data. Secondly, there’s likely to be a `/users/<id>/posts` endpoint that returns all the posts for a user. The third endpoint will then be the `/users/<id>/followers` that returns a list of followers per user.

![REST example](images/graphQL-vs-API-0.png)

In GraphQL on the other hand, you’d simply send a single query to the GraphQL server that includes the concrete data requirements. The server then responds with a JSON object where these requirements are fulfilled.

![GraphQL example](images/graphQL-vs-API-1.png)

### REST Problems That GraphQL Solves

#### Overfetching: Downloading unnecessary data

- Overfetching means that a client downloads more information than is actually required in the app. Imagine for example a screen that needs to display a list of users only with their names.
- In a REST API, this app would usually hit the /users endpoint and receive a JSON array with user data. This response however might contain more info about the users that are returned, e.g. their birthdays or addresses - information that is useless for the client because it only needs to display the users’ names.

#### Underfetching and the n+1 problem

- Underfetching generally means that a specific endpoint doesn’t provide enough of the required information. The client will have to make additional requests to fetch everything it needs.
- This can escalate to a situation where a client needs to first download a list of elements, but then needs to make one additional request per element to fetch the required data.

#### Rapid Product Iterations on the Fronten

- Thanks to the flexible nature of GraphQL, changes on the client-side can be made without any extra work on the server. Since clients can specify their exact data requirements, no backend engineer needs to make adjustments when the design and data needs on the frontend change.

#### Insightful Analytics on the Backend

- As each client specifies exactly what information it’s interested in, it is possible to gain a deep understanding of how the available data is being used. This can for example help in evolving an API and deprecating specific fields that are not requested by any clients any more.

#### Benefits of a Schema & Type System

- GraphQL uses a strong type system to define the capabilities of an API. All the types that are exposed in an API are written down in a schema using the GraphQL Schema Definition Language (SDL). This schema serves as the contract between the client and the server to define how a client can access the data.
- Once the schema is defined, the teams working on frontend and backends can do their work without further communication since they both are aware of the definite structure of the data that’s sent over the network.
- Frontend teams can easily test their applications by mocking the required data structures. Once the server is ready, the switch can be flipped for the client apps to load the data from the actual API.

## Core Concepts

//TODO finish using the sandbox in the core concepts page: https://www.howtographql.com/basics/2-core-concepts/