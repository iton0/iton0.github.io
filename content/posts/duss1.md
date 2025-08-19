+++
draft = false
date = 2025-08-19T15:12:14-04:00
title = "Working on duss Pt 1"
description = ""
slug = ""
authors = []
tags = ["duss"]
categories = ["devlog"]
externalLink = ""
series = []
+++

# Intro

I'm starting a new personal project called duss to sharpen my backend development skills. This project will be more complex than my last one, HkUp, and will showcase the progression of my abilities to potential employers.

# All the fuss about duss

duss is an acronym for *distributed url shortening service*.

- **What's a URL shortening service?** It's a tool that takes a long, complicated web address and converts it into a shorter, more manageable link. When someone clicks the short link, they are automatically redirected to the original, long URL. This is useful for making links easier to share, especially on social media, and for tracking link clicks.

- **Why distributed?** My goal is to build a system that can handle a large number of requests reliably and efficiently. A distributed system means that the service is spread across multiple servers, making it more robust and scalable. This approach addresses challenges like high availability (the service is always online, even if one server fails) and performance optimization, which are critical for a real-world application.

---

### Phase 1: Planning and Design

Before writing any code, I invested a few days into planning the system's architecture. This phase is crucial for ensuring the final product is robust, scalable, and built on a solid foundation.

**1. Defining Core Features & Constraints**

I outlined the minimum viable product (MVP) and a few "nice-to-have" features to aim for later:

* **Must-Haves:**
    * Shorten a long URL and generate a unique key.
    * Redirect a short URL to the original long URL.
* **Nice-to-Haves:**
    * Basic analytics (e.g., click counts).
    * Allow for custom, user-defined short keys.

**2. Choosing the Technology Stack**

I selected a technology stack that would directly support a distributed architecture:

* **Go & Gin:** Go's built-in concurrency features and Gin's high-performance routing are perfect for building fast, lightweight microservices.
* **PostgreSQL:** This will serve as my primary, persistent database. Its reliability and structured nature are ideal for storing the canonical URL mappings.
* **Redis:** An in-memory key-value store. It will be used as a distributed cache to handle the high volume of redirection requests with minimal latency.
* **Docker:** Essential for containerizing each service, making them portable and easy to run in any environment.
* **Railway:** A modern cloud platform with native support for my entire tech stack, from Go to managed PostgreSQL and Redis services, making deployment seamless.

**3. Designing the Microservices Architecture**

To tackle the distributed challenge directly, I decided against a monolithic approach. My final architecture will consist of three distinct services, each with a single responsibility:

* **URL Shortener Service:** The "write" service, handling new URL creation.
* **URL Redirect Service:** The "read" service, designed for high-speed lookups and redirection.
* **Key Generation Service:** An internal service to ensure unique short keys without a database bottleneck.

This design allows each component to be independently scaled and maintained.

**4. Planning the API Endpoints**

Based on this architecture, I planned the API endpoints that would be split across my different services:

* **`POST /api/v1/shorten`**: This will be handled by the **URL Shortener Service**. It will accept a long URL and return a new short URL.
* **`GET /:shortKey`**: This will be handled by the **URL Redirect Service**. It will take a short key and issue a redirect to the original URL.

With the architecture planned and the technologies selected, the foundation is now complete. I'm ready to begin the build process, starting with the core services in the next phase.
