# MenuGen Assistant (LLM Version)

## Overview

**MenuGen Assistant** is a minimal, LLM-native implementation of the idea behind *MenuGen*, the “vibe-coded” application developed by Andrej Karpathy.

It takes a photo of a restaurant menu and generates visual representations of each dish directly from the text — no traditional web app required.

This project demonstrates how a purely prompt-driven approach can replicate the core functionality of a full-stack application.

---

## Context

As described by Andrej Karpathy in his blog:

👉 [https://karpathy.bearblog.dev/sequoia-ascent-2026/](https://karpathy.bearblog.dev/sequoia-ascent-2026/)

> “MenuGen was a traditional web app: take a picture of a restaurant menu, OCR the dish names, generate images of the dishes, and render the result in a UI. It required frontend code, APIs, image generation, deployment, auth, payments, secrets, and infrastructure.
>
> But later, I saw the Software 3.0 version: take a photo of the menu, give it to a multimodal model, and ask it to render dish images directly onto the menu image.”

---

## What This Project Is

This repository is an **LLM-only implementation** of MenuGen:

* No frontend
* No backend
* No APIs
* No infrastructure

Just:

* A short set of instructions (prompt)
* A multimodal model (ChatGPT / Claude / Gemini)
* A menu image

---

## Key Idea

Instead of building software around the task, we **describe the task to the model**:

* Extract menu text (with verification)
* Interpret dishes
* Generate representative images
* Pair each image with the exact original text

---

## Why This Matters

This project illustrates the shift from:

**Software 2.0 (code + models)**
→ **Software 3.0 (instructions + models)**

What previously required:

* Engineering effort
* Deployment pipelines
* UI/UX work
* Integrations

…can now be achieved in **under 15 minutes** using a well-designed prompt.

Works with Claude Projects and ChatGPT Projects using the same instructions.

Gemini Gem required modified instructions and is slower in image generation for menu items than two other systems (as of May 10, 2026). 

---

## Repository Structure

```
/
├── instructions.md             # Instructions for Claude project and ChatGPT project or Gemini Gem.
├── instructions_gemini_gem.md  # Instructions for Gemini Gem
├── README.md                   # This file
├── example/           
│   ├── original_menu.png       # Input menu image (Spago Beverly Hills restaurant)
│   └── generated_menu.pdf      # Output menu with dish images + text
└── setup/
    ├── claude_projects.md
    ├── gemini_gems.md
    └── chatgpt_projects.md
```

---

## How It Works

1. Upload a menu image
2. The model:

   * Extracts and verifies text (no hallucination)
   * Breaks menu into individual items
   * Generates images per item
   * Displays image + exact corresponding text
   
3. Output is rendered directly in the chat interface

---

## Development Time

* "Development" time for an instruction prompt and one test: **< 15 minutes**
* Validate that it works as Claude Project, ChatGPT project: **< 10 minutes**
* Debugging Gemini's behavior and modifying instructions: **30 minutes** 
* No code required beyond prompt design

---

## Note on Gemini Gem

Instructions that worked for Claude and ChatGPT projects did not work for Gemini Gem. 
Instead of generating images it generated verbal description of the images.

Gemini gave the following explanation:
```
The reason the AI defaulted to making up fake Markdown links instead of generating real images is due to batching constraints. 
Image generation tools (like my Nano Banana 2 model) require significant processing power. 
If an AI is instructed to generate 10–12 images in a single response, it usually hits a built-in safety or timeout limit. 
To avoid failing the prompt entirely, the model "cheats" by generating fake web links that look like images in the text editor.
```

With modified instruction it works, but takes significantly longer than two other LLM systems even in Gemini's "Fast" mode.

---

## License

MIT License. See LICENSE for details.