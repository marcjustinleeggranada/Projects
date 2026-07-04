<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Add Custom Slots to a Lex Chatbot

**Project Link:** [View Project](http://nextwork.ai/projects/aws-ai-lex2)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Add Custom Slots to a Lex Chatbot

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex2_c4fc89af)

---

## Introducing Today's Project!

In today's project, I used Amazon Lex to build and configure a banking chatbot called BankerBot that helps users check their account balances. Specifically, I created a custom slot type to capture account types like checking and savings, integrated these slots into the CheckBalance intent, and customized error handling using FallbackIntent message variations to ensure a smooth, secure conversation flow.

### What is Amazon Lex?

Amazon Lex is a fully managed service on AWS for building conversational interfaces using voice and text, and it is useful because it provides advanced natural language understanding and automatic speech recognition, allowing us to easily build lifelike chatbots that capture intents and slots from natural user phrasing without needing deep machine learning expertise.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how seamlessly the natural language parsing in Amazon Lex would extract slot information directly from a user's initial message. I was surprised that simply saying "check my savings" allowed the chatbot to immediately recognize and record the savings value into the slot values table, completely skipping the dedicated account question prompt and making the dialogue feel incredibly fluid and intuitive.

### This project took me...

This project took me about 60 minutes to complete from start to finish. Most of my time was spent configuring the custom slot types in Amazon Lex and testing how the chatbot extracts values from my utterances, which was a very smooth and rewarding hands-on learning experience.

---

## Slots

Slots are pieces of information that a chatbot needs to complete a user's request. Think of them as blanks that need to be filled in a form.

By adding custom slots in utterances, my chatbot's users can experience a much more natural and efficient conversation because they can provide key details—like their account type—right in their opening statement. This allows Amazon Lex to auto-fill the slot values immediately, saving users time by skipping unnecessary follow-up prompts and getting them straight to their bank balance.

In today's project, I created a custom slot type to collect specific bank account choices like checking, savings, or credit from users. Setting up this custom slot type in Amazon Lex allows my chatbot to validate user inputs and restrict choices to the exact account types we support, preventing conversational errors and ensuring a smoother user experience.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex2_97dc2351)

---

## Connecting slots with intents

This slot type has restricted slot values, which means Amazon Lex will only validate and accept the exact values we set—Checking, Savings, and Credit—instead of using machine learning to allow other entries. Restricting these values ensures the chatbot only handles supported account types, preventing users from holding conversations about banking options we do not actually offer.

I associated my custom slot with the CheckBalance intent, which is the action designed to help users retrieve their bank account details. This connection allows Amazon Lex to recognize when a user wants to check their money, prompting them specifically to provide their accountType so the chatbot gathers the precise information needed to fulfill their inquiry.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex2_c4fc89af)

---

## Slot values in utterances

I included slot values in some of the utterances (i.e. user inputs) by referencing the slot name inside curly braces directly within my sentences. For example, I added sample utterances like "What is the balance in my {accountType} account?" which allows Amazon Lex to extract the user's desired account type immediately from their initial message without needing to prompt them for it separately.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex2_505be5b8)

---

## Handling failures in slot values

I added variations for the dateOfBirth slot prompt, such as "For verification, what is your date of birth?" followed by "Please enter your birth date so we can secure your account." The messages play in order, so my end user will see the friendlier greeting first, and then the more direct security-focused prompt if they fail to provide a valid date format, guiding them to answer correctly in Amazon Lex.

I set up failure responses by customizing the closing response of the FallbackIntent within Amazon Lex. I also used failure responses to guide lost users back on track by listing supported tasks, like checking a bank balance or transferring funds. A default setting I changed was replacing the generic system error message with friendly, customized message variations so that our customers always receive helpful instructions when the chatbot doesn't understand them.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-ai-lex2_a028bc8d2)

---

---
