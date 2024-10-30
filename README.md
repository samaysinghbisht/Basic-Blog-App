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

### Using Kubernetes:
To start the app locally, ensure you have Kubernetes installed. Each service has its own `Dockerfile` for easy containerization.

1. Clone the repository:
   ```bash
   git clone https://github.com/samaysinghbisht/Basic-Blog-App.git
   cd Basic-Blog-App
2. Install Ingress-Nginx Controller by following this documentation: [LINK](https://kubernetes.github.io/ingress-nginx/deploy/#quick-start)

3. Once that is done, We need to update our hosts configuration so that localhost requests get routed to **posts.com** otherwise we will get an error in our frontend application, so please update your **etc/hosts/** file and add this at the end of the file:
   ```
   127.0.0.1 posts.com
4. Deploy the application in your kubernetes cluster by following below commands:
   ```bash
   kubectl create namespace blog
   kubectl apply -f infra/k8s/
5. Now navigate to **posts.com** in your browser and enjoy.


## Architecture Diagram of the application:

![architecture](https://github.com/user-attachments/assets/0936eba0-5b11-4eff-aea1-c8e70626e327)

## Routing rules within the application:

![routes](https://github.com/user-attachments/assets/bb7f83bf-8da2-4ebe-9ec8-c6536a857748)

