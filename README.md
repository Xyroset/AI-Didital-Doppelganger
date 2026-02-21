# **🤖 Personal AI Telegram Bot (LLM + Voice + Vision)**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Xyroset/AI-Didital-Doppelganger/blob/main/Personal_AI_Telegram_Bot_(LLM_%2B_Voice_%2B_Vision).ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Ever wanted to clone yourself, your friend, or just build the ultimate custom AI assistant directly in Telegram? That's exactly what this project does. 

I put together this Colab notebook so you can spin up a fully multimodal AI companion for free using Google Colab's T4 GPU. It reads texts, listens to voice memos, looks at pictures, and replies with realistic voice messages. It’s essentially your own local pocket AI.

---

## ✨ What makes it cool?
* 🧠 **Actually Smart:** Uses a local LLM running right in Colab. No need to pay for expensive OpenAI API keys.
* 🗣️ **Cloned Voice:** Talks back to you with a custom voice using Coqui XTTS.
* 👁️ **Sees Your Memes:** Send it photos, GIFs, or stickers. It uses Groq's Vision API to understand exactly what it's looking at.
* 👂 **Hears You:** Send a voice message, and it instantly transcribes and replies in context.
* ⚡ **Context Aware:** It actually remembers your conversation (and you can wipe its memory anytime with a simple command).

---

## 🛠️ Under the Hood
Here is the tech stack powering the bot:
* **[Unsloth](https://github.com/unslothai/unsloth):** Makes running Heavy LLMs super fast and efficient on Colab's T4 GPU.
* **[Coqui XTTS](https://github.com/coqui-ai/TTS):** The magic behind the text-to-speech and zero-shot voice cloning.
* **[Groq API](https://console.groq.com/):** Does the heavy lifting for lightning-fast image recognition (`llama-3.2-11b-vision-preview`) and audio transcription (`whisper-large-v3-turbo`).
* **[Aiogram](https://docs.aiogram.dev/):** The engine keeping the Telegram bot running smoothly.

---

## 🗂️ Getting Your Models
To make this work, you'll need to drop two things into your Google Drive: a "Brain" (LLM) and a "Voice" (TTS model).

### 1. The Brain (LLM)
Grab any Unsloth-compatible model (like a 4-bit Llama-3 or Mistral to save RAM) from [Hugging Face](https://huggingface.co/models?search=unsloth) and upload the folder to your Drive.
* **Want it to sound exactly like you?** You can actually fine-tune an LLM on your own exported Telegram or Discord chats! The [Unsloth GitHub](https://github.com/unslothai/unsloth) has awesome, free Colab notebooks to do this in just a few minutes. 

### 2. The Voice (TTS)
You need an XTTS model folder containing a `config.json`, the model weights, and a clean 10-15 second audio clip of the voice you want to clone (make sure to name it `reference.wav`).
* **The Quick Way:** Grab the base `coqui/XTTS-v2` model from Hugging Face. XTTS is crazy good at "zero-shot" cloning it'll just copy the voice from your `reference.wav` without any extra training.
* **The Pro Way:** If the zero-shot clone sounds a bit off or has the wrong accent, you can fine-tune it. I highly recommend [xtts-finetune-webui by daswer123](https://github.com/daswer123/xtts-finetune-webui). It’s a super simple web interface for training XTTS on your own audio datasets.

---

## 🚀 Let's Get It Running

1. **Get your Tokens:** Grab a bot token from [@BotFather](https://t.me/BotFather) on Telegram and a free API key from the [Groq Console](https://console.groq.com/).
2. **Drive Setup:** Upload your LLM and TTS model folders to your Google Drive.
3. **Open Colab:** Click that blue "Open in Colab" badge at the top of this page. Make sure the runtime is set to **T4 GPU** (`Runtime` -> `Change runtime type`).
4. **Hide your keys:** Click the 🔑 **Secrets** tab on the left sidebar in Colab. Add `BOT_API` and `GROQ_API`, paste your keys, and turn ON "Notebook access" for both. (Never paste keys directly into the code!)
5. **Run the Blocks:**
   * Run **Block 1** (it'll install the required libraries and restart the session).
   * Fill out your folder paths and tweak the AI sliders in **Block 2**.
   * Run **Block 3** (this loads the heavy models into memory, so go grab a coffee ☕).
   * Run **Block 4**. Once the console says `Bot is running!`, jump into Telegram and type `/start`.

---

## 📝 Commands
* `/start` - Wake up the bot.
* `/voice_mode` - Toggle between text and voice message replies.
* `/reset` - Regenerate the last response if you didn't like what the AI said.
* `/reset_memory` - Wipe the current conversation context and start fresh.

---

## 📜 License
This project is open-source and available under the [MIT License](LICENSE). 
*Note: The AI models used in conjunction with this code (like Llama, XTTS, etc.) are subject to their own respective licenses and terms of use.*
