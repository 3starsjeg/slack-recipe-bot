# Slack Recipe Bot — n8n Automation

## Overview

This project is an n8n automation that works as a recipe assistant directly inside Slack.

A user sends a recipe name or recipe request in the `#n8nautomation` Slack channel. The workflow captures the message, sends it to an AI model, generates a short list of required products and ingredients with approximate quantities, and sends the result back to the same Slack channel.

## Workflow

Slack Trigger → Capture Recipe → Basic LLM Chain → Slack Send Message

The workflow contains the following nodes:

1. **Slack Trigger**
   - Triggers when a new message is posted in the selected Slack channel.
   - Monitors the `#n8nautomation` channel.
   - Ignores messages from the bot to prevent unnecessary self-triggering.

2. **Capture Recipe**
   - Captures the recipe request from the Slack message.
   - Stores the recipe message in the `recipe` field.
   - Stores the Slack channel ID in the `channelId` field.

3. **Basic LLM Chain**
   - Uses an AI model to understand the user's recipe request.
   - Handles requests such as `give chicken briyani recipe`.
   - Can understand minor spelling mistakes and common phrases around recipe requests.
   - Generates a clear, short, bulleted list of products and ingredients.
   - Includes approximate quantities.
   - If the recipe cannot be identified, asks the user to rephrase the recipe name.

4. **OpenAI Chat Model**
   - Provides the language model used by the Basic LLM Chain.
   - The model is connected to the Basic LLM Chain as its chat model.

5. **Send Recipe to Slack**
   - Sends the AI-generated ingredient list back to the same Slack channel where the request was received.

## Example

User sends in Slack:

`give chicken briyani recipe`

The bot responds with a practical ingredient list such as:

- 500 g chicken
- 2 cups basmati rice
- 2 onions
- 2 tomatoes
- 1/2 cup yogurt
- Ginger-garlic paste
- Green chilies
- Mint and coriander
- Biryani masala
- Cooking oil or ghee
- Whole spices
- Salt and other required ingredients

## Requirements

- n8n
- Slack workspace
- Slack app/bot
- Slack API credential configured in n8n
- AI model credential configured in n8n

## Credentials and Security

Credentials are stored in n8n rather than directly inside the workflow logic.

Do not add Slack Bot Tokens, Slack Signing Secrets, OpenAI API Keys, passwords, or other secret credentials to this repository.

The exported workflow contains credential references used by n8n, not the actual secret API key values.

## Setup

1. Import the workflow JSON into n8n.
2. Configure the Slack API credential.
3. Configure the AI model credential.
4. Make sure the Slack bot is installed in the workspace.
5. Invite the bot to the `#n8nautomation` channel.
6. Configure Slack Event Subscriptions with the appropriate n8n webhook URL.
7. Verify that the Slack Trigger receives new messages.
8. Activate/publish the workflow.
9. Send a recipe request in `#n8nautomation` and verify that the bot responds.

## Expected Result

The completed automation allows a user to request a recipe in Slack and receive a concise list of the products and ingredients required to make it, without leaving Slack.

## Project Purpose

This project demonstrates an n8n automation that combines Slack event handling, data processing, an AI language model, and an automated Slack response into one workflow.
