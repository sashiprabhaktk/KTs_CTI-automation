# A to Z Setup Guide: KT's CTI Workflow

This guide will walk you through setting up the Automated Cyber Threat Intelligence (CTI) workflow from scratch.

## 📋 Prerequisites

Before you begin, ensure you have the following installed and running:

1.  **n8n**: The workflow automation tool.
    *   [Installation Guide](https://docs.n8n.io/hosting/installation/)
2.  **Ollama**: For running the AI model locally.
    *   [Download Ollama](https://ollama.com/download)
3.  **Discord Account**: To create webhooks for receiving alerts.

---

## 🚀 Step 1: Prepare the AI Model (Ollama)

This workflow uses the **Phi3** model for summarization.

1.  Open your terminal/command prompt.
2.  Run the following command to download and start the model:
    ```bash
    ollama run phi3
    ```
3.  Keep Ollama running in the background.

---

## 🚀 Step 2: Set Up Discord Webhooks

You need a Discord server where you want to receive the news.

1.  Open Discord and go to your Server Settings.
2.  Navigate to **Integrations** > **Webhooks**.
3.  Click **New Webhook**.
4.  Name it (e.g., "CTI Alerts") and select the channel.
5.  Click **Copy Webhook URL**. Save this for later.
6.  *Optional*: Create 4 separate webhooks if you want to route news from different sources to different channels (TechRadar, BleepingComputer, SecurityWeek, TheHackerNews).

---

## 🚀 Step 3: Import the n8n Workflow

1.  Open your n8n dashboard in your browser.
2.  Click on the **Workflows** tab.
3.  Click **Add Workflow** > **Import from File**.
4.  Select the `KT's CTI.json` file from this repository.

---

## 🚀 Step 4: Configure Credentials in n8n

The exported workflow has placeholders for credentials. You must update them:

### 1. Ollama Configuration
1.  Find the **Ollama Model** nodes (there are 4).
2.  Click on a node and go to **Credentials**.
3.  Create a new **Ollama API** credential.
4.  Set the **Base URL** (usually `http://localhost:11434` or `http://host.docker.internal:11434` if using Docker).

### 2. Discord Configuration
1.  Find the **Discord** nodes (Discord, Discord1, Discord2, Discord3).
2.  Click on a node.
3.  Under **Authentication**, ensure **Webhook** is selected.
4.  Paste your **Webhook URL** (copied in Step 2) into the URL field.
5.  Repeat this for all 4 Discord nodes.

---

## 🚀 Step 5: Test and Activate

1.  Click the **Test Workflow** (or **Execute Workflow**) button at the bottom of the n8n editor.
2.  If everything is configured correctly, you should receive summarized news in your Discord channel!
3.  Once verified, toggle the **Active** switch at the top right to start the schedule.

---

## 🛠️ Troubleshooting

*   **Ollama connection failed**: Ensure Ollama is running and the Base URL in n8n is correct.
*   **Discord message not sent**: Double-check your Webhook URL and ensure the n8n container/server has internet access.
*   **No news items**: Some RSS feeds might be empty if there are no new articles today. Try changing the "Limit" nodes temporarily to test.

---

Enjoy your automated CTI updates!
