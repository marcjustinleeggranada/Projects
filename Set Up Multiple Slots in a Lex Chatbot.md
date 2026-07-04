<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up Multiple Slots in a Lex Chatbot

**Project Link:** [View Project](http://nextwork.ai/projects/aws-ai-lex5)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Build a Chatbot with Multiple Slots

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex5_67890123)

---

## Introducing Today's Project!

### What is Amazon Lex?

Amazon Lex is a fully managed artificial intelligence service for building conversational interfaces with voice and text, and it is useful because it leverages advanced natural language understanding to easily capture user inputs, manage complex dialogue states, and deploy intelligent chatbots that automate tasks like fund transfers and balance inquiries.

### How I used Amazon Lex in this project

In today's project, I used Amazon Lex to configure an advanced TransferFunds intent that utilizes a shared custom slot type for multiple slot inputs. I also set up confirmation prompts to verify transaction details before fulfillment and deployed the completed chatbot resources in seconds using AWS CloudFormation.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how incredibly fast it would be to deploy a complex chatbot using AWS CloudFormation. Seeing our custom intents, slots, and backend integrations automatically spin up from a single code template in seconds was amazing, though I also didn't expect to troubleshoot a backend permission block that required adding a resource-based policy to grant Amazon Lex access to our AWS Lambda function.

### This project took me...

This project took me about 45 minutes to complete, which was highly efficient considering how much we accomplished. Most of my time was spent setting up the multiple slots and configuring the confirmation prompts within Amazon Lex, but utilizing AWS CloudFormation to deploy the entire backend stack in seconds saved an incredible amount of time and simplified the overall deployment.

---

## TransferFunds

An intent I created for my chatbot was TransferFunds, which helps users transfer money between their bank accounts by gathering essential details like the source account, the target account, and the transfer amount using multiple slots, and then presenting a confirmation prompt to repeat the transaction details back to the user before final fulfillment.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex5_67890123)

---

## Using multiple slots

For this intent, I had to use the same slot type twice. This is because both the source and target accounts for a transfer require the exact same set of valid bank account values, such as checking or savings. Reusing a single custom `accountType` slot type for both the source and target `slots prevents redundant configurations, simplifies bot maintenance, and ensures Amazon Lex validates both values against the same predefined choices.

I also learnt how to create confirmation prompts, which are specialized messages in Amazon Lex that repeat gathered slot values back to the user to verify their details. They are crucial because they act as a safety check, allowing the chatbot to get explicit user agreement before moving to intent fulfillment or canceling the transaction if the user declines.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex5_97dc2351)

---

## Exploring Lex features

Lex also has a special conversation flow feature that visually maps out each step of a chatbot interaction in a logical, chronological order. This dynamic diagram updates automatically as you edit your intent configurations, displaying current slots and prompts, while also providing clickable recommendations for optional dialogue paths that make designing natural user interactions much simpler.

A visual builder is a drag-and-drop flowchart tool in Amazon Lex that lets you design conversational paths visually. It helps you build an intent from scratch by mapping slots, prompts, and paths on a visual canvas.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex5_12345678)

---

## AWS CloudFormation

AWS CloudFormation is a service that gives you an easy way to define, deploy, and manage your cloud resources using infrastructure as code. It is extremely useful because it automates the setup of entire environments in seconds, allowing you to reliably deploy and scale your resources—such as Amazon Lex chatbots and AWS Lambda functions—without having to configure them manually in the console one by one.

I used AWS CloudFormation to automate the setup and deployment of my BankerBot chatbot resources using infrastructure as code. This allowed me to upload a single YAML template and automatically configure the intents, custom slots, and backend AWS Lambda connections in seconds instead of clicking through multiple pages in the AWS console manually.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex5_c4fc89af)

---

## The final result!

Re-building my bot with CloudFormation took me only a few minutes, which was incredibly fast compared to configuring each intent and slot manually in the console. Using an infrastructure as code template through AWS CloudFormation automated the entire setup process, instantly deploying the Amazon Lex chatbot and linking it to the backend AWS Lambda function without any repetitive manual steps.

There was an error after I deployed my bot! The error was a denied access message when testing the CheckBalance intent, which happened because the permissions on the AWS Lambda function did not allow the chatbot to trigger it. I fixed this by going to the permissions tab of my BankingBotEnglish function and adding a new resource-based policy statement with the statement ID my-custom-permission-amazonlexchatbot, which successfully granted the Amazon Lex principal permission to invoke the function.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex5_505be5b8)

---

## Using the visual builder

Using the visual builder, I added a new Get slot value card directly into the TransferFunds conversation flow. What this means for an end user is a smoother, more intuitive experience where the chatbot dynamically captures missing transaction details in real time, preventing confusing error loops and guiding them naturally to a successful transfer.

The new Get slot value card will trigger when the conversation flow reaches the node where Amazon Lex needs to collect a specific piece of mandatory information from the user. This card will try to capture a designated slot value, such as the accountType, by prompting the user with a question and parsing their response to verify that it matches the configured slot type criteria before allowing the conversation to proceed.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex5_9cac15cd4)

---

---
