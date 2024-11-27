# Conversational-AI-Chatbot-for-Mobile-Wallet-App
We're seeking an experienced Conversational AI developer to design and implement a chatbot for our innovative mobile wallet application. The chatbot will assist users with:

- Transactional inquiries (balance, history, etc.)
- Financial goal setting and budgeting
- Educational content (financial literacy)
- Basic customer support

Key Requirement:

No Data Collection: The chatbot must operate without collecting, storing, or transmitting any user data. All data will remain locally stored on the user's device.

Responsibilities:

1. Design and develop conversational flows.
2. Implement natural language processing (NLP) for intent recognition and entity extraction.
3. Integrate chatbot with existing app infrastructure (APIs, SDKs).
4. Ensure scalability, security, and compliance with financial regulations.
5. Collaborate with our UI/UX team.

Requirements:

1. 3+ years of experience in Conversational AI development.
2. Proficiency in Dialogflow, Rasa, or similar platforms.
3. Strong knowledge of NLP, machine learning, and AI principles.
4. Experience with mobile app development (iOS, Android).
5. Familiarity with financial industry regulations.
6. Kotlin Expertise.

Nice to Have:

1. Experience with financial chatbots or mobile wallet apps.
2. Knowledge of cloud-based services (AWS, Google Cloud).
3. Certification in Conversational AI or related fields.

Important Note:

Due to client restrictions, developers from Pakistan are not eligible for this project. We appreciate your understanding.

Deliverables:

1. Fully functional chatbot integrated with the mobile app.
2. Documented codebase and conversation flows.
3. Testing and quality assuranc
============================
Python code template that demonstrates the foundation for implementing a local-only chatbot for your requirements. The chatbot operates on the user's device without collecting or transmitting data, ensuring privacy compliance. For this, we’ll leverage the Rasa framework, which supports local processing of intents and entities.
Prerequisites

    Install Rasa:

    pip install rasa

    Mobile Integration: You will need to integrate the Rasa chatbot with your mobile wallet app using SDKs or APIs that support Kotlin.

Folder Structure

Rasa projects follow a specific folder structure. Before coding, ensure the directory contains:

    domain.yml: Defines intents, entities, and responses.
    nlu.yml: Contains training examples for intents.
    stories.yml: Contains conversation flow examples.
    actions.py: Custom action logic.

Code Template
1. Domain File (domain.yml)

Define chatbot intents, entities, and responses.

version: "3.1"
intents:
  - check_balance
  - transaction_history
  - set_budget
  - financial_education
  - customer_support

entities:
  - budget
  - goal

responses:
  utter_greet:
    - text: "Hi! How can I assist you today?"
  utter_check_balance:
    - text: "Your current balance is $500."
  utter_transaction_history:
    - text: "Here are your recent transactions: $20 at Store A, $50 at Store B."
  utter_set_budget:
    - text: "Your budget has been set to {budget}."
  utter_financial_education:
    - text: "Saving 10% of your income is a good start. Would you like to learn more?"
  utter_customer_support:
    - text: "I'm here to help! Please describe your issue."

actions:
  - action_set_budget

2. NLU Data (nlu.yml)

Train the chatbot with examples of user input for intent recognition.

version: "3.1"
nlu:
  - intent: check_balance
    examples: |
      - What is my current balance?
      - Show me my balance.
      - How much money do I have?

  - intent: transaction_history
    examples: |
      - Show me my transaction history.
      - What are my recent transactions?
      - List my past payments.

  - intent: set_budget
    examples: |
      - Set my budget to $500.
      - I want a monthly budget of $1000.
      - Change my budget to $300.

  - intent: financial_education
    examples: |
      - How can I save more money?
      - Teach me about financial planning.
      - I want to learn financial literacy.

  - intent: customer_support
    examples: |
      - I need help.
      - My app isn't working.
      - How can I contact support?

3. Stories (stories.yml)

Define conversation patterns for different intents.

version: "3.1"
stories:
  - story: check balance
    steps:
      - intent: check_balance
      - action: utter_check_balance

  - story: transaction history
    steps:
      - intent: transaction_history
      - action: utter_transaction_history

  - story: set budget
    steps:
      - intent: set_budget
      - action: action_set_budget

  - story: financial education
    steps:
      - intent: financial_education
      - action: utter_financial_education

  - story: customer support
    steps:
      - intent: customer_support
      - action: utter_customer_support

4. Custom Actions (actions.py)

Define logic for dynamic responses.

from typing import Any, Text, Dict, List
from rasa_sdk import Action, Tracker
from rasa_sdk.executor import CollectingDispatcher

class ActionSetBudget(Action):

    def name(self) -> Text:
        return "action_set_budget"

    def run(self, dispatcher: CollectingDispatcher,
            tracker: Tracker,
            domain: Dict[Text, Any]) -> List[Dict[Text, Any]]:
        
        budget = next(tracker.get_latest_entity_values("budget"), None)
        if budget:
            dispatcher.utter_message(text=f"Your budget has been set to {budget}.")
        else:
            dispatcher.utter_message(text="I didn't catch your budget. Could you please specify?")
        
        return []

5. Training the Model

Run the following command to train the chatbot:

rasa train

6. Testing the Chatbot

To test locally:

rasa shell

7. Integration with Kotlin

Once the chatbot is functional, integrate it with the mobile wallet app:

    Use Rasa REST API for communication between the app and the chatbot.
    Kotlin's HTTP libraries (e.g., OkHttp) can send user input to Rasa and retrieve responses.

Notes for Compliance

    Data Storage: Ensure all user data remains in memory during the chatbot session and does not persist on the server.
    Financial Regulations: Validate all chatbot responses for compliance with local financial laws.
    Localization: If the app is multi-lingual, train the chatbot with multilingual data.

This framework establishes the foundation for your chatbot. Customize intents, responses, and integrations as needed for your specific application.
