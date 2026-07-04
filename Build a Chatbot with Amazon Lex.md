<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Chatbot with Amazon Lex

**Project Link:** [View Project](http://nextwork.ai/projects/aws-ai-lex1)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Build a Chatbot with Amazon Lex

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex1_505be5b8)

---

## Introducing Today's Project!

### Project overview

In this project, I will demonstrate how to build and test a functional banking chatbot called BankerBot using Amazon Lex by configuring intents, sample utterances, and natural fallback responses. I'm doing this project to learn the foundational principles of conversational AI and gain hands-on experience designing engaging user interfaces for advanced backend integrations.

### What is Amazon Lex?

Amazon Lex is a fully managed artificial intelligence service from AWS designed to build conversational interfaces into applications using voice and text. By utilizing advanced natural language processing and automatic speech recognition, it enables developers to create highly engaging, human-like chatbot experiences without requiring deep machine learning or speech synthesis expertise.

### Key tools and concepts

Services I used were Amazon Lex. Key concepts I learnt include configuring intents using custom sample utterances, setting the confidence score threshold, managing conversational failures gracefully with FallbackIntent and message variations, and establishing conversational flow using initial responses.

### Personal reflections

"One thing I didn't expect in this project was how dynamically Amazon Lex handles conversational variations. I was surprised that a simple confidence score threshold of 0.40 controls whether the bot successfully matches a greeting or routes the user to the FallbackIntent, showing how much complex natural language processing is happening under the hood."

### Project timeline

This project took me approximately 60 minutes to complete. The most challenging part was understanding how the confidence score threshold determines when the FallbackIntent is triggered. It was most rewarding to test my chatbot in Amazon Lex and see it successfully choose from different message variations to greet users naturally.

---

## Setting up a Lex chatbot

### Approach to chatbot setup

In this step, I will create a blank chatbot named BankerBot using Amazon Lex and configure its basic settings, such as the IAM role permissions, idle session timeout, and voice because establishing this core bot infrastructure is the essential foundation I need before I can build custom intents, set up sample utterances, or integrate backend logic.

### Chatbot creation process

I created my chatbot from scratch with Amazon Lex. Setting it up took me just around 5 minutes.

### IAM role configuration

While creating my chatbot, I also created a role with basic permissions because it will need to interact later with services such as Lambda.

### Intent classification confidence score

In terms of the intent classification confidence score, I kept the default value of 0.40. This means that the chatbot needs to be at least 40% confident that it understands what the user is asking to be able to give a response.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex1_97dc2351)

---

## Intents

In this step, I will create and configure the WelcomeIntent with sample greetings because it trains my chatbot to recognize when a user wants to start a conversation. By setting up a custom closing response, I ensure that my bot welcomes users with a friendly, helpful greeting right away in Amazon Lex.

### Creating my first intent

An intent is what the user is trying to achieve in their conversation with the chatbot. For example, checking a bank account balance; booking a flight; ordering food.

I created my first intent, WelcomeIntent, to recognize when a user wants to start a conversation.

### Testing chatbot responses

I launched and tested my chatbot, which could respond successfully if I enter explicit utterances like 'Hi' or 'Hello', as well as similar expressions like 'Help me' and 'Hiya'. Because Amazon Lex uses natural language understanding with a confidence threshold of 0.40, it successfully matched these similar inputs to my WelcomeIntent and returned my configured greeting.

---

## Handling unrecognized inputs

My chatbot returned the error message 'Intent FallbackIntent is fulfilled' when I entered 'how are you' and 'good morning' because these expressions scored below my bot's 0.40 confidence score threshold for the WelcomeIntent. Since Amazon Lex could not match these inputs to any of my custom greetings with at least 40% confidence, it triggered the default FallbackIntent to handle the unrecognized input.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex1_505be5b8)

---

## Configuring FallbackIntent

In this step, I will customize the closing responses and add message variations for the FallbackIntent because it replaces confusing default errors with user-friendly instructions. This ensures that when a user's input falls below our 0.40 confidence score threshold, our Amazon Lex chatbot can dynamically guide them back to supported tasks like finding account balances or transferring funds.

### When FallbackIntent triggers

FallbackIntent is a default intent in every chatbot that gets triggered when a user's input cannot be matched to any of the custom intents we have defined. In Amazon Lex, this happens if the calculated confidence score for all other intents falls below our configured threshold of 0.40, indicating the bot does not understand the input and needs to deliver a helpful fallback response.

I wanted to configure FallbackIntent because the default response 'Intent FallbackIntent is fulfilled' is robotic and confusing for users. By customizing this intent with helpful instructions and conversational variations, I can gently guide users back to supported tasks—like checking a balance or transferring funds—ensuring they don't get stuck in a dead-end conversation with Amazon Lex.

### My FallbackIntent configuration

To configure FallbackIntent, I located it in the left navigation panel of Amazon Lex and scrolled down to Closing responses. I expanded the response options, replaced the default text with a descriptive helper message, and then added optional message variations to keep the conversational flow natural before saving and rebuilding my chatbot.

I also added variations! What this means for an end user is that they will not experience a repetitive, robotic loop if the chatbot fails to understand their input. Instead of hearing the exact same default error message every single time, Amazon Lex will dynamically choose from my different configured variations. This makes the conversation feel much more natural, engaging, and human-like while guiding them back to supported banking features.

---

## FallbackIntent with Variations

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex1_c4fc89af)

---

## Initial Responses

In this project extension, I'm about to configure initial responses for my bot's intents. I'm doing this so that my chatbot immediately acknowledges the user's intent with a friendly confirmation, making Amazon Lex feel more responsive and human-like during conversational transitions.

### Setting up initial responses

Initial responses are immediate messages that a chatbot sends the moment an intent is triggered, confirming to the user that their request has been recognized before the bot starts asking for more details. I've set up initial responses for my intents in Amazon Lex so that the conversational flow feels instantly responsive, active, and natural from the very first input.

### Initial response implementation

The initial response messages I set up are instant acknowledgments that trigger the moment an intent like the FallbackIntent is identified. For the user, this means they receive immediate feedback that the bot has recognized their input, removing any conversational lag and reassuring them that Amazon Lex is working to guide them back to supported tasks.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex1_09bcb9701)

---

---
