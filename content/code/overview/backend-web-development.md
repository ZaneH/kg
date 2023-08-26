---
title: Backend Web Development
tags: backend, code
---

## The Rundown

Similar to frontend development, backend web development relies on essential technologies that form the backbone of robust web applications. These tools handle data, logic, and server operations. The most popular tools I see in the current job market are Golang and Node.js. Golang is better in performance and Node.js is more accessible to devs (because it uses JavaScript.) [[code/languages/rust|Rust]] has been growing in popularity for it's type-safety and superior performance but there are not as many jobs available yet.

### Requirements

- **Code Editors (e.g., VSCode):** Use efficient code editors for coding convenience.
- **Server-Side Languages (e.g., Golang, Ruby, Node.js):** Master languages that power server-side operations. There are a lot of options here, Node.js is likely the most popular. Golang is also a popular choice for its performance.
- **Databases (e.g., SQL, NoSQL):** Learn data storage techniques and different database types.
- **APIs:** Understand APIs for seamless communication between components.
	- There are lots of [free APIs](https://github.com/public-apis/public-apis) you could use to practice API calls.
	- Playing around with AWS S3 would be good practice.
- **Version Control (e.g., Git):** Use version control tools for collaboration and code management.
- **Authentication and Security:** Implement security measures like user authentication.
- **Server Deployment and Hosting:** Learn to deploy and host applications.
	- Deploying to AWS and working through the entire process is pretty difficult the first 2 times. It's great practice and becomes much easier once you have a flow.
	- There are other options, but AWS is an industry standard.
- **Testing and Debugging:** Test, debug, and optimize code for functionality and performance.
    - Understanding how to identify and mitigate bottlenecks is a valuable skill here.
- **Command Line:** Command line skills for server tasks and automation.
- **Docker**: Package an entire project into an "image" that can be ran in a "container."
	- Valuable for getting a project on your local machine running in the cloud.

Stay adaptable and keep learning as backend technologies evolve. This toolkit equips you to create resilient web applications that work in tandem with frontend development to deliver excellent user experiences.

> [!info]
> 
> Similar to tools like Figma in frontend development, backend developers often utilize tools like Postman or Swagger for testing and documenting APIs. These tools enhance the efficiency of backend development by facilitating API design, testing, and documentation.

## Good to Know

These are not vital for backend web development, but they are good to know about and can do cool things.

- **WebSockets (and/or [[code/topics/socketio-info|socket.io]]):** Enable real-time, bidirectional communication between clients and servers, making interactive features like live notifications and messaging possible.
- **Threads:** Dive into multithreading to execute multiple tasks concurrently, improving application performance and responsiveness by utilizing the capabilities of modern processors.
- **Serverless Computing:** Explore serverless platforms like AWS Lambda, Azure Functions, or Google Cloud Functions to build and deploy applications without worrying about server management, scaling, or provisioning.
- **Microservices Architecture:** Understand the concept of breaking down applications into smaller, independent services that communicate with each other, providing scalability, fault isolation, and easier maintenance.
- **Message Queues (e.g., RabbitMQ, Kafka):** Learn about asynchronous communication between different parts of your application, enhancing decoupling and improving scalability.
- **Webhooks:** Use webhooks to trigger events in other applications, enabling seamless communication between applications.

A full list of projects I find interesting that relate to backend programming can be found in this [GitHub list](https://github.com/stars/ZaneH/lists/api-tools). You may also be interested in the [DevOps & Infra list](https://github.com/stars/ZaneH/lists/devops-and-infra) which has its own role in modern software.