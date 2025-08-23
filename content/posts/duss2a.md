+++
draft = false
date = 2025-08-21T22:43:09-04:00
title = "Working on duss Pt 2a"
description = ""
slug = ""
authors = []
tags = []
categories = ["devlog"]
externalLink = ""
series = ["duss-devlog"]
+++

*This is the first of two posts on my progress with phase 2 of the duss timeline.*

I'm excited to share that I've completed the URL redirect service, a crucial component of this phase. In this post, I'll walk you through the process of building the service, discuss some of the technical challenges I overcame, and highlight a few of the valuable lessons I learned along the way.

# Microservices

To start this phase, I first needed to define its structure. In my [previous post]({{< relref "posts/duss1" >}}), I explored the high-level concepts and use cases of distributed systems.

As I conducted further research, the term microservices frequently appeared, causing some initial confusion. I was looking for general distributed system designs, but I discovered that microservices are, in fact, a specific type of distributed system.

Understanding that a microservice is a specific implementation of a distributed system, much like a square is a specific type of parallelogram, I began to structure my project.

While microservices are typically spread across multiple repositories in an enterprise setting, I decided to use a monorepo. For a personal project, this approach makes more sense, simplifying the tooling and allowing me to manage all services in one place.

#### Service Directories

Each service in this project is an independent Go module, acting as a self-contained microservice.

- `cmd/server/main.go`: The entry point for the service.
- `internal/api/handlers.go`: Manages the service's API endpoints.
- `internal/core/services`: Contains the core business logic, isolated from other services.
- `internal/infrastructure/storage`: Holds the specific storage implementations, like PostgreSQL or Redis.
- `internal/infrastructure/web`: Contains the service's web-facing components.

To see the full implemenation view the [ARCHITECTURE.md](https://github.com/iton0/duss/blob/main/ARCHITECTURE.md).

#### API Endpoints

Based on the project's architecture, the API is designed to be split across different microservices, with each endpoint serving a specific, isolated purpose. This is a core tenet of the microservices approach and allows for independent development, deployment, and scaling. For the URL redirect service specifically, the API is simple and focused on a single responsibility: redirecting a user to the correct URL. Its only public-facing endpoint is the Redirect to Original URL endpoint, which uses a GET method to look up the shortKey in either the Redis cache or the PostgreSQL database and then issues a 301 (Permanent) redirect to send the user to the original long URL. This straightforward design allows for a single-purpose service that can be highly optimized for performance, which is critical for a redirect function.

# Why I'm Using Docker

Although I haven't implemented Docker yet, it's a foundational piece of this project's architecture. My plan is to use it to containerize each microservice. This approach offers several key benefits that are essential for a distributed system like duss.

#### Consistent Environments

One of the biggest challenges in software development is the "it works on my machine" problem. Docker solves this by packaging the application and all its dependencies into a single, isolated container. For this project, it means I can define the exact environment for each Go service, including its dependencies and runtime libraries. This ensures that what works on my local machine will also work consistently in any other environment, from testing to production. This consistency is crucial when you have multiple, interconnected services.

#### Service Isolation and Portability

Each of my microservices will have a distinct purpose. Docker allows me to isolate each service, like the URL redirect service, within its own container, preventing conflicts between their dependencies and resources. This is a core principle of microservices. Furthermore, these containers are lightweight and portable, meaning I can easily move them across different systems, whether it's my local machine, a virtual machine, or a cloud server.

#### Streamlined Development and Deployment

Docker Compose will be the backbone of my local development environment. By defining all services—the three Go applications, PostgreSQL, and Redis—in a single docker-compose.yml file, I can spin up the entire application stack with one command. This simplifies the onboarding process and makes it easy to run the full system. In the future, this same orchestration file can serve as a template for more complex deployments using tools like Kubernetes, allowing the project to scale gracefully.

# Testing

Testing each microservice independently was a key part of this phase. This microservice architecture naturally lends itself to a well-defined testing strategy. Because each service has a single responsibility, it's easier to write comprehensive unit tests for its core business logic.

I focused on black-box testing for the API endpoints and unit testing for the core logic within the internal/core/services directory. For example, the url-redirect-service's tests ensure it performs the correct lookup and redirect.

To isolate the services during testing, I implemented mock storage repositories within the internal/infrastructure/storage/mock directory. This allows me to test the service's logic without needing a live database or Redis instance, making tests faster and more reliable. I can simulate database interactions and test edge cases, like a key not being found, without the external dependency. This approach not only speeds up the development cycle but also ensures that the tests are robust and truly test the business logic, not the infrastructure.

# Conclusion

Completing the URL redirect service has been an illuminating journey into the practical application of microservices. The project is now a more concrete example of a distributed system, with distinct services communicating to achieve a single goal. The experience has reinforced the value of a monorepo for personal projects—it provides the architectural benefits of microservices while keeping the development and deployment overhead low.

A major takeaway from this phase is the importance of clear service contracts and dependency isolation. By defining a shared/ directory for common data models, I've ensured consistency across services without creating tight coupling. Similarly, the use of Docker has made managing the entire system a breeze, turning a complex setup into a repeatable, one-command process.

In the next post I will continue working on finishing phase 2 of the timeline
by building the URL shortening service.
