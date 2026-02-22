<div align="center">
  <img src="assets/Preview.png" height="400">
</div>

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

## 🎬 See It In Action: Johnny Silverhand Clone
<div align="center">
  <video src="https://github.com/user-attachments/assets/9ab8e780-2626-4d5e-8b3c-dbb4e7f9e841" width="600" controls></video>
</div>

---

**What it took to build this specific clone:**
* 🧠 **LLM Dataset:** Only **120 lines of dialogue** used for fine-tuning the personality.
* 🗣️ **TTS Audio:** Just a **30-second clean audio clip** for the voice engine.

⚠️ **Pro Tip on Quality:** This example was made with very minimal data to show how accessible this is. However, the final quality of your bot's personality and voice depends *entirely* on the volume and quality of your dataset. A larger text history and a studio-quality audio sample (without background noise or music) will make your digital clone sound incredibly realistic!

---

## 🛠️ Under the Hood
Here is the tech stack powering the bot:
* **[Unsloth](https://github.com/unslothai/unsloth):** Makes running Heavy LLMs super fast and efficient on Colab's T4 GPU.
* **[Coqui XTTS](https://github.com/coqui-ai/TTS):** The magic behind the text-to-speech and zero-shot voice cloning.
* **[Groq API](https://console.groq.com/):** Does the heavy lifting for lightning-fast image recognition (`meta-llama/llama-4-scout-17b-16e-instruct`) and audio transcription (`whisper-large-v3-turbo`).
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
3. **Open Colab:** Click that blue "Open in Colab" badge at the top of this page. Make sure the runtime is set to **T4 GPU** (`Runtime` => `Change runtime type`).
4. **Hide your keys:** Click the 🔑 **Secrets** tab on the left sidebar in Colab. Add `BOT_API` and `GROQ_API`, paste your keys, and turn ON "Notebook access" for both. (Never paste keys directly into the code!)
5. **Run the Blocks:**
   * Run **Block 1 (Install)**. It will download the required libraries and automatically restart the session.
   * Set up **Block 2 (Settings)**. Paste your folder paths and tweak the AI sliders.
     * ⚠️ **Important LLM Loading Settings:** To avoid Out Of Memory (OOM) errors on a 15GB T4 GPU, adjust the Unsloth parameters based on your model:
       * **7B-9B Models (Llama-3, DeepSeek):** `LLM_MAX_SEQ_LENGTH` = 2048, `LLM_LOAD_IN_4BIT` = True.
       * **12B Models (Mistral-Nemo):** `LLM_MAX_SEQ_LENGTH` = 2048, `LLM_LOAD_IN_4BIT` = True.
       * **1.5B-3B Models (Qwen):** `LLM_MAX_SEQ_LENGTH` = 8192, `LLM_LOAD_IN_4BIT` = False.
   * Run **Block 3 (Load Models)**. This loads the heavy weights into the GPU and spins up the TTS server.
   * Customize **Block 4 (Personalization)**. Here you can completely change the bot's core personality (`SYSTEM_INSTRUCTION`), adjust the typing debounce timer, and translate all UI messages (like "Typing..." or "Generating voice...") to fit your style.
   * Run **Block 5 (Start Telegram bot)**. Once the console says `Bot is running!`, jump into Telegram and type `/start`.

---

## 📝 Commands
* `/start` - Wake up the bot.
* `/voice_mode` - Toggle between text and voice message replies.
* `/reset` - Regenerate the last response if you didn't like what the AI said.
* `/reset_memory` - Wipe the current conversation context and start fresh.

---

## 🤝 Support & Feedback

<h2 align="center">
  If you had fun building your own AI companion or just found this project useful, I’d massively appreciate a ⭐️ Star on this repository! <br><br>
  It helps more people discover the project and keeps me motivated to push more cool AI stuff. ♥ <3
</h2>

<br>

**Something broke? Got a killer feature idea?** Don't be shy, let's make this bot even better together:
* 🐛 Open an **Issue** right here on GitHub if you catch any bugs or OOM errors.
* 💬 Hit me up on Telegram: [@Just_Xirexxx](https://t.me/Just_Xirexxx)
* 📧 Drop me an email: [xyroset+dev@gmail.com]([xyroset+dev@gmail.com)

Pull requests and forks are always welcome. Let's build the ultimate open-source pocket AI together! 🚀

---

## 📜 License
This project is open-source and available under the [MIT License](LICENSE). 
*Note: The AI models used in conjunction with this code (like Llama, XTTS, etc.) are subject to their own respective licenses and terms of use.*
