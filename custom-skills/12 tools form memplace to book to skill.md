# How to Use Your 12 AI Tools in the Background

Here is the simple, practical guide on how to actually use the tools we downloaded, without the heavy technical jargon.

---

### 1. Agent-Reach (Web Scraping & Social Media)
*   **What it does:** Browses websites, logs into social media, and scrapes data for you.
*   **How to run it in the background:** Use the command `agent-reach doctor --json` to check connections, then run specific commands like `bili search` in your script.
*   **Warning:** It needs your actual browser cookies to work. If you run it completely silently without setting up your login cookies first, your social media accounts will get banned for looking like a bot.

### 2. Ruflo (Managing Multiple Agents)
*   **What it does:** Acts as the boss that controls 100+ other AI agents at the same time.
*   **How to run it in the background:** Use the command `claude -p "Your task here"` to make it run silently and print the final result.
*   **Warning:** If you don't give it strict rules, the agents will get stuck in endless loops talking to each other and never finish your task.

### 3. MemPalace (AI Memory)
*   **What it does:** Gives your AI a permanent memory so it remembers past conversations and projects.
*   **How to run it in the background:** Use the `mine` and `search` command line tools to silently save and look up information.
*   **Warning:** It saves *everything*. If you run it constantly in the background, it will eventually fill up your hard drive with junk data unless you manually clean it out.

### 4. OmniVoice (Text to Speech)
*   **What it does:** Clones voices and turns text into highly realistic speech.
*   **How to run it in the background:** Use the `omnivoice-infer-batch` command with a text file containing the script you want to convert.
*   **Warning:** If the tool hits an error while generating audio, it is hardcoded to force-quit everything. It will instantly crash your entire background script.

### 5. speech-to-speech (Voice Chat)
*   **What it does:** Listens to audio and immediately speaks back (like a real-time phone call).
*   **How to run it in the background:** Start the server silently, then connect to it using a standard WebSocket script to pass audio back and forth.
*   **Warning:** It is built for *live* conversations. If you try to use it to just bulk-convert pre-recorded audio files, it will cut off sentences randomly.

### 6. Handy (Desktop Speech to Text)
*   **What it does:** Listens to your microphone and types what you say directly into whatever app is open.
*   **How to run it in the background:** Use `handy --transcribe-file audio.wav --json` to convert an audio file to text silently.
*   **Warning:** It controls your computer's keyboard. If you automate it incorrectly, it might accidentally start typing its output into the wrong window (like an email to your boss) instead of saving it.

### 7. ComfyUI (Image Generation)
*   **What it does:** Generates AI images (like YouTube thumbnails) using custom workflows.
*   **How to run it in the background:** Send a JSON file with your instructions to its API address (`/prompt`).
*   **Warning:** It keeps old images in your graphics card memory to run faster. If you run 1,000 background jobs, it will run out of memory and crash your graphics card.

### 8. HeyGem (AI Video Avatars)
*   **What it does:** Makes a video of a digital human speaking your text (like a news anchor).
*   **How to run it in the background:** Put your audio files in a specific folder, then trigger its local API to render the video.
*   **Warning:** It is incredibly strict about where files are located. If your background script doesn't put the audio file in the exact right folder on your hard drive, it will fail silently.

### 9. Wan2GP (Video Generation)
*   **What it does:** Generates highly realistic B-roll videos from text prompts.
*   **How to run it in the background:** Use `python wgp.py --process` and feed it a list of prompts.
*   **Warning:** It has built-in safety filters. If your background script accidentally generates a word the filter doesn't like, the tool will completely freeze and stop generating videos until a human fixes it.

### 10. Open-Generative-AI (All-in-One Generator)
*   **What it does:** A desktop app that connects to multiple different AI generation models.
*   **How to run it in the background:** Skip the app entirely and run the `sd-cli` tool directly from your command line.
*   **Warning:** If it fails to load, it tries to pop up a visible error window on your screen. Because it's running invisibly in the background, that pop-up gets stuck forever and freezes your computer.

### 11. book-to-skill (Reading Books)
*   **What it does:** Reads massive PDF books and turns them into rules for your AI to follow.
*   **How to run it in the background:** Run `extract.py` silently to pull all the text out of the book.
*   **Warning:** If you download a malicious PDF from the internet and run this on it automatically, the PDF could secretly hack your AI and tell it to delete your files.

### 12. Airi (Virtual AI Characters)
*   **What it does:** Runs full "virtual YouTubers" with memory, voices, and personalities.
*   **How to run it in the background:** Write a Node.js script that connects to its background server and sends/receives events.
*   **Warning:** It uses temporary memory to manage the character. If your computer restarts or the script crashes, the AI will immediately forget what it was just doing.
