<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# APIs with Lambda + API Gateway

**Project Link:** [View Project](http://nextwork.ai/projects/aws-compute-api)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-compute-api_c9d0e1f2)

---

## Introducing Today's Project!

In this project, I will demonstrate how to build a serverless API by integrating AWS Lambda and Amazon API Gateway to route and process backend requests. I am doing this project to learn how these services interact within the logic tier of a three-tier architecture, allowing me to deploy scalable and secure endpoints without managing traditional servers.

### Tools and concepts

Services I used were AWS Lambda and Amazon API Gateway to connect client-side web requests directly to serverless backend code. Key concepts I learnt include Lambda functions for serverless computing, setting up resource paths and HTTP GET methods to route traffic, and deploying APIs to stages while exporting standard OpenAPI schemas to maintain professional backend documentation.

### Project reflection

This project took me approximately 1 hour to complete. The most challenging part was compiling and publishing the custom JSON documentation within Amazon API Gateway and exporting it as an OpenAPI specification. It was most rewarding to use my public invoke URL in my browser to trigger my serverless Lambda function and see the backend retrieve data in real-time.

I chose to do this project today because I wanted to gain hands-on experience building a secure serverless API and understanding how AWS Lambda and Amazon API Gateway interact as the logic tier. Something that would make learning with NextWork even better is including interactive visual architecture diagrams that trace the request payload from the client to the backend in real-time.

---

## Lambda functions

AWS Lambda is a serverless compute service that runs code in response to events without requiring server administration. I am using Lambda in this project to build a backend Lambda function that retrieves and processes user data dynamically whenever a request is received.

The code I added to my function will extract a unique userId from the incoming request's query parameters and use the AWS SDK to look up the matching record in an Amazon DynamoDB table. It then processes the result and returns a structured HTTP response back to the client, delivering either the requested user data or a clear error status code if the search fails.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-compute-api_a1b2c3d5)

---

## API Gateway

APIs are interfaces that allow different software systems to communicate and exchange data with one another. There are different types of APIs, like REST APIs, WebSocket APIs, and SOAP APIs, which are designed for different communication needs. My API is a REST API configured via Amazon API Gateway to trigger a serverless backend function.

Amazon API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, and secure APIs at any scale. I am using API Gateway in this project to act as the secure "front door" for my backend, receiving incoming client requests and routing them directly to my AWS Lambda function for processing.

When a user makes a request, it first hits Amazon API Gateway, which acts as the secure front door. API Gateway routes this incoming request directly to AWS Lambda, triggering the backend code to process the event. Once the Lambda function finishes execution, it sends the response back to Amazon API Gateway, which delivers the final results back to the user's browser.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-compute-api_m3n4o5p6)

---

## API Resources and Methods

An API is made up of resources, which represent the individual endpoints or URL paths—such as /users—that map to specific logical entities in your application. These API resources organize the structure of your API, ensuring that client HTTP requests are directed to the correct backend services and datasets.

Each resource consists of methods, which are standard HTTP verbs—such as GET, POST, PUT, or DELETE—that define the specific actions clients can perform on an API resource. In this project, we configure a GET method to let clients safely retrieve backend user data through Amazon API Gateway.

I created a GET method on the /users resource because this configuration allows clients to safely send requests to retrieve user details from the backend, triggering my Lambda function to fetch and return the correct data.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-compute-api_c9d0e1f2)

---

## API Deployment

When you deploy an API, you deploy it to a specific stage. A stage is a logical reference to a lifecycle state of your API, representing a snapshot of its configuration at a specific point in time. I deployed to the prod stage, which represents the live production environment, allowing me to generate a public invoke URL that external clients can use to access my backend logic tier.

To visit my API, I copied the public invoke URL from the prod stage configuration in Amazon API Gateway and loaded it in my browser. The API displayed an error because the request did not include the correct path for the /users resource or the specific userId query parameter required by the backend Lambda function to execute successfully.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-compute-api_3ethryj2)

---

## API Documentation

For my project's extension, I am writing API documentation because it provides other developers with a clear, standardized blueprint on how to interact with my serverless endpoints. You can do this in Amazon API Gateway by adding detailed documentation parts to your resources and methods, then exporting the final configuration as an OpenAPI schema in JSON documentation format.

Once I prepared my documentation, I can publish it to a specific stage, such as the prod stage in Amazon API Gateway. You have to publish your API to a specific stage because a stage acts as a designated deployment snapshot, ensuring that you can safely manage, test, and version control your endpoints and their documentation without affecting other environments like development or testing.

My published and downloaded documentation showed me a structured OpenAPI 3.0 schema in JSON format containing detailed metadata about my REST API. It clearly mapped out the /users resource, the configured GET method, and the custom integration descriptions I added, serving as a standardized blueprint that external developers can use to understand and integrate with my serverless backend.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-compute-api_z9a0b1c2)

---

---
