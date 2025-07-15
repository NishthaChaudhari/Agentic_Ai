# Agentic_Ai
# LinkedIn Agent with Images

A fully automated **n8n** workflow that lets you compose, iterate, and publish custom LinkedIn posts—complete with AI-generated visual assets—via a simple Telegram chat interface.

---
![Workflow_AgenticAI](https://github.com/user-attachments/assets/83621b19-4a2a-4ce4-8480-c47ec9fdbd2f)

##  Overview

1. **User Input**  
   - **Telegram Trigger**: Listens for text or voice messages in your Telegram bot.  
   - **Switch**: Routes text vs. voice input.  
   - **Set Text / Transcribe**: Extracts text directly or uses OpenAI’s Whisper to transcribe audio.

2. **Human-in-the-Loop Text Generation**  
   - **Content Creation Agent**: Crafts an initial LinkedIn post draft using GPT-4.  
   - **Set Post**: Stores the draft.  
   - **Feedback Request**: Sends the draft back to the user via Telegram and waits for “publish” vs. “iterate” feedback.  
   - **Feedback Evaluation**: Classifies the user’s reply.  
   - **Iteration Agent**: If changes are requested, loops back to refine the post.

3. **Image Generation**  
   - **Create Image Prompt**: Reads the final post and constructs a detailed prompt for a supporting visual infographic.  
   - **Generate Image**: Uses OpenAI’s image API (GPT-Image-1) to produce a professional graphic.

4. **Publishing**  
   - **LinkedIn Node**: Publishes the text + image to your LinkedIn profile as a public post.

---

## 📦 Prerequisites

- **n8n** (v1.x or later) installed and running  
- A Telegram bot with API token  
- An **OpenAI** account (API key)  
- A **LinkedIn** OAuth2 application (Client ID & Secret)  
- A **Tavily Search** API key (for real-time web lookups)  

---

## ⚙️ Installation & Setup

1. **Import the Workflow**  
   - In your n8n Editor, click **Import** → paste the provided JSON (`Linkedin_Agent_with_Images.json`) → **Save**.

2. **Configure Credentials**  
   - **Telegram Trigger / Telegram** node → paste your **Bot Token**.  
   - **OpenAI** nodes → enter your **OpenAI API Key**.  
   - **LinkedIn** node → set up OAuth2 (Client ID, Client Secret, Redirect URI).  
   - **Tavily Search** node → add `Authorization: Bearer <YOUR_TAVILY_KEY>`.

3. **Adjust Prompt Templates (optional)**  
   - Open each LangChain **Agent** node to tweak system messages, instructions, or model versions.

4. **Activate the Workflow**  
   - Toggle the workflow **Active** in the top right corner of the n8n Editor.

---

## 📝 Node Reference

| Section                   | Node Name               | Purpose                                                         |
|---------------------------|-------------------------|-----------------------------------------------------------------|
| **User Input**            | Telegram Trigger        | Receive text or voice from user                                 |
|                           | Switch                  | Route by input type                                             |
|                           | Set Text                | Capture text payload                                            |
|                           | Telegram → OpenAI       | Transcribe voice → text                                         |
| **Text Generation**       | Content Creation Agent  | Generate LinkedIn post draft (GPT-4.1 via LangChain)            |
|                           | Set Post                | Store the draft                                                 |
|                           | Feedback Request        | Send draft back to user for approval                            |
|                           | Feedback Evaluation     | Classify reply as “Publish” or “Iterate”                        |
|                           | Iteration Agent         | Revise draft per user feedback                                  |
| **Image Generation**      | Create Image Prompt     | Build AI-image prompt based on final post                       |
|                           | Generate Image          | Produce the graphic (GPT-Image-1 via OpenAI)                    |
| **Publishing**            | LinkedIn                | Post final text + image publicly on LinkedIn                    |

---

## 🛠️ Usage

1. **Chat a Post Idea**  
   - Send a message (or voice note) to your Telegram bot describing the post topic.

2. **Review & Iterate**  
   - You’ll receive a draft. Reply **“Publish”** to go live, or any other feedback to refine.

3. **Automatic Publishing**  
   - Once approved, your post and image are published to LinkedIn instantly.

---

## 🔧 Customization

- **Model Versions**: Swap between `gpt-4.1`, `gpt-4o-mini`, or other supported LLMS.  
- **Prompt Tuning**: Edit system messages in each agent for tone or format changes.  
- **Image Styles**: Tweak the “Create Image Prompt” guidelines to produce charts, icon sets, or metaphoric illustrations.  

---

## 🤝 Contributing

Feel free to open issues or pull requests to:

- Support additional languages or platforms  
- Integrate other image-generation APIs  
- Add more nuanced feedback classifications  

---
