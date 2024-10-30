# Basic Blog App

A basic blog application built using React and Node.js with Express. This project follows a microservices architecture, where different services handle specific tasks and communicate via an event bus. Each service is dockerized, making it easy to deploy and scale independently.

## Features
- **Frontend (React):** Displays posts and comments, checks for moderation tags ("CommentApproved" and "CommentRejected").
- **Comments Service (Express):** Allows users to add comments to posts.
- **Event Bus (Express):** A simple event bus that receives and routes events between services.
- **Moderation Service (Express):** Moderates comments and adds the "CommentModerated" tag based on disallowed words.
- **Query Service (Express):** Provides the posts and comments to the frontend, ensuring data is displayed even if other services are down. It handles pending events when back online.

## Services & Ports
- **Client (React)** - Runs on port `3000`
- **Comments Service** - Runs on port `4001`
- **Posts Service** - Runs on port `4000`
- **Moderation Service** - Runs on port `4003`
- **Query Service** - Runs on port `4002`
- **Event Bus** - Runs on port `4005`

## Architecture
- **Microservices:** Each service performs a distinct role and communicates with others via events.
- **Event-Driven:** The event bus is the core of communication between services. Events are dispatched and processed asynchronously.
- **Resilient Query Service:** Even if other services go down, the Query Service ensures that posts and comments are available on the frontend.

## How to Run

### Using Docker
To start the app locally, ensure you have Docker installed. Each service has its own `Dockerfile` for easy containerization.

1. Clone the repository:
   ```bash
   git clone https://github.com/samaysinghbisht/Basic-Blog-App.git
   cd Basic-Blog-App

2. Build each service by navigating to their repository, for example:
   ```bash
   cd client
   docker build -t <tag> .
   docker run -p 3000:3000 <tag>
   
3. Perform above steps for each service, keeping in mind the port mapping:
   ```bash
   Posts --> -p 4000:4000
   Comments --> -p 4001:4001
   Query --> -p 4002:4002
   Moderation --> -p 4003:4003
   Event-Bus --> -p 4005:4005

### Using Docker-Compose:
To start the app locally using docker-compose, build the images locally using the above commands and the run below command to start the app:
   ```bash
   docker compose up