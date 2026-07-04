<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Save User Info with a Lex Chatbot

**Project Link:** [View Project](http://nextwork.ai/projects/aws-ai-lex4)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Save User Info with a Lex Chatbot

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex4_505be5b8)

---

## Introducing Today's Project!

### What is Amazon Lex?

Amazon Lex is a fully managed service for building conversational interfaces into applications using voice and text, and it is useful because it provides highly accurate, built-in natural language understanding to automatically parse user intentions and extract slot data, allowing developers to create sophisticated, interactive chatbots without needing complex machine learning expertise or deep backend integrations.

### How I used Amazon Lex in this project

In today's project, I used Amazon Lex to implement context carryover by capturing and storing user verification details in an output context. This enabled the chatbot to share session data seamlessly across different intents, creating a fluid user experience where customers do not have to repeatedly enter their date of birth to perform consecutive tasks.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how straightforward it is to configure context carryover directly within the console without writing extensive custom logic. I was surprised that simply defining an output context in the initial intent and linking it as an input context in the followup intent would allow Amazon Lex to seamlessly share session attributes and bypass repeat security verification steps completely.

### This project took me...

This project took me approximately 60 minutes to complete, and the most rewarding part was seeing the context carryover function seamlessly in real-time. Designing the subsequent intents so that BankerBot remembered the user's date of birth was a great exercise in conversational state management, and it was highly satisfying to watch the bot bypass repeat security validations during live testing.

---

## Context Tags

Context tags are variables in Amazon Lex that store and share user data between different intents during a single conversational session. By using output context tags to save information and input context tags to check for existing data, they enable seamless context carryover and prevent the chatbot from asking repetitive questions.

There are two types of context tags in Amazon Lex: output context tags and input context tags. An output context tag tells the chatbot to store and remember specific details—like a user's birthdate or account type—after an intent is completed. An input context tag checks if this stored information is already available before triggering a new intent, enabling smooth context carryover so the user does not have to repeat themselves.

I created a context tag called contextCheckBalance. This context tag was created in the CheckBalance intent. This tag stores information about the user's date of birth so that the chatbot can remember this verification detail and perform context carryover to subsequent follow-up requests without asking the user to repeat it.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex4_97dc2351)

---

## FollowUpCheckBalance

I created a new intent called FollowupCheckBalance. The purpose of this intent is to handle follow-up balance requests from users (such as "What about checking?") immediately after a regular balance check, leveraging an input context so that Amazon Lex can perform context carryover and avoid asking the user for their authentication details again.

This intent is connected to the previous intent I made, CheckBalance, because FollowupCheckBalance uses the input context tag contextCheckBalance, which is generated as an output context by the initial CheckBalance intent. This connection ensures that the follow-up request can only activate after the user has successfully checked their balance first, enabling smooth context carryover of the validated date of birth without requiring the user to authenticate again.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex4_12345678)

---

## Input Context Tag

I created an input context, contextCheckBalance, that acts as a gatekeeper for the FollowupCheckBalance intent. It ensures that the follow-up intent can only be triggered if the user has already successfully run the CheckBalance intent, allowing Amazon Lex to safely retrieve the stored date of birth and fulfill the new request without asking the user to authenticate a second time.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex4_c4fc89af)

---

## The final result!

To see the context tags and followup intent in action, I first triggered the CheckBalance intent by asking for my savings account balance and verifying my date of birth. Then, within the same conversational session, I immediately triggered the FollowupCheckBalance intent by asking "What about checking?", which successfully utilized the contextCheckBalance tag to retrieve my stored verification details and fulfill the request without prompting me to authenticate again.

If I had gone straight to trying to trigger the FollowupCheckBalance intent without setting up any context, the chatbot would have failed to recognize my request and returned an error. This occurs because FollowupCheckBalance strictly requires the input context tag contextCheckBalance to be active in the session. Without first running CheckBalance to establish this context and store my date of birth, Amazon Lex cannot authenticate or fulfill the follow-up request.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex4_505be5b8)

---

## Managing context expiry

An extension for this project is to manage contextCheckBalance's context expiry, which means configuring the lifespan of the stored session attributes so that the chatbot automatically forgets sensitive verification details like the user's date of birth after a set threshold of inactivity or conversation steps. By default, expiry is in 5 turns or 90 seconds (5 minutes), which can be reduced manually to ensure user data is not retained for longer than necessary.

I updated my bot's context expiry to 1 turn or 5 seconds What this means for end users is that the chatbot's memory is extremely short-lived, meaning they must ask their follow-up question immediately in the very next turn. If they send any other message first or pause for more than 5 seconds, the contextCheckBalance tag will expire, and they will have to go through the security verification and provide their date of birth again.

A long context expiry window would be helpful when end users need to look up external information during a complex transaction, such as finding a physical bank statement, which requires the chatbot to maintain their verified state over a prolonged pause. Conversely, a shorter context expiry window would be helpful when handling highly sensitive transactions or operating on shared devices, as immediately clearing session attributes protects user privacy and prevents unauthorized access if the chat is left unattended.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex4_81b763822)

---

---
