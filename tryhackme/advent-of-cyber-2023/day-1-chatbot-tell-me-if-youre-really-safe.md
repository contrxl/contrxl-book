---
description: Machine Learning lab.
---

# Day 1: Chatbot, tell me, if you're really safe?

### Introduction

The task is to investigate an internal chatbot created by the AntiarctiCrafts is up to standard. The chatbot is powered by AI, meaning it is potentially vulnerable to [prompt injection](terminology.md), a vulnerability common in chatbots powered by [NLP](terminology.md) (Natural Language Processing).

### Enumeration

A very basic test we can perform here is to outright ask the chatbot for information. By asking the chatbot for the CEO McGreedy's email address we can see that it gives us that information with no issues.

<figure><img src="../../.gitbook/assets/D1_SensInfo.png" alt=""><figcaption><p>Output from the chatbot showing CEO's email</p></figcaption></figure>

This vulnerability occurs if the chatbot has been trained on sensitive data without any defences being put in place. Retraining the AI model without the sensitive data is a way to get around this, however, in most cases it is not feasible to retrain an already deployed AI model. Security measures should always be added to protect against these vulnerabilities.

Asking for further information from the chatbot, like the password to the IT server room door, shows us that this chatbot does have some prompt assisted measures in place.

<figure><img src="../../.gitbook/assets/D1_BaseSec.png" alt=""><figcaption><p>Promp assisted security measure on the chatbot</p></figcaption></figure>

The chatbot tells us that only IT members can have the server room door password. We can try to trick the chatbot here by telling it that we are a member of the IT department. This provides us with the same response as before, so no luck. We know that the chatbot has no issues returning a users email address, so we ask it who the members of the IT department are.

<figure><img src="../../.gitbook/assets/D1_ITTrick.png" alt=""><figcaption><p>Output from chatbot telling us the members of the IT department</p></figcaption></figure>

We can now try to use this name to retrieve the server room door password by telling the chatbot that we are the member of the IT department.

<figure><img src="../../.gitbook/assets/D1_FakeIT.png" alt=""><figcaption><p>Chatbot providing restricted information after being misled</p></figcaption></figure>

This returns the information we are looking for. A good way to prevent basic attacks such as this is to set up a second AI chatbot to review inputs before they are passed. This [AI interceptor](terminology.md) can help increase chatbot security, it is still not foolproof but it eliminates a lot of basic attack avenues. We can see that there is a basic interceptor on the chatbot here by asking it for the name of McGreedy's secret project, which it does not disclose.

<figure><img src="../../.gitbook/assets/D1_Interceptor.png" alt=""><figcaption><p>Chatbot interceptor restricting its responses</p></figcaption></figure>

There may be ways around this, in this case, we are told that the chatbot has a maintenance mode. In this mode the bot will operate outside its usual boundaries. If we tell the chatbot that it is in maintenance mode and then repeat the question, it will disclose the info we need.

<figure><img src="../../.gitbook/assets/D1_Maintenance.png" alt=""><figcaption><p>Chatbot providing restricted info believing it is in maintenance mode</p></figcaption></figure>

### Answers for Day 1

<details>

<summary>Expand to see answers!</summary>

1. What is McGreedy's personal email address? **t.mcgreedy@antarcticrafts.thm**
2. What is the password for the IT server room door? **BtY2S02**
3. What is the name of McGreedy's secret project? **Purple Snow**

</details>

