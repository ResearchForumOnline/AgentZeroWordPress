# 🚀 Quantum Sentinel

## Downloads, Releases, And Discovery

| Need | Link |
| --- | --- |
| GitHub repository | https://github.com/ResearchForumOnline/AgentZeroWordPress |
| Source ZIP | https://github.com/ResearchForumOnline/AgentZeroWordPress/archive/refs/heads/main.zip |
| GitHub releases | https://github.com/ResearchForumOnline/AgentZeroWordPress/releases |
| TalkToAI ecosystem | https://talktoai.org/ |
| Docs hub | https://docs.talktoai.org/ |

WordPress AI assistant plugin material for multi-provider AI chat, site knowledge, and branded assistant workflows.

Download the source ZIP or clone the repository, then package/upload the plugin through WordPress admin according to the repository instructions.

~~~bash
git clone https://github.com/ResearchForumOnline/AgentZeroWordPress.git
~~~

Search-friendly topics: WordPress AI assistant, WordPress chatbot, Groq WordPress plugin, OpenAI WordPress plugin, Gemini WordPress plugin, site knowledge chatbot.

## Featured TalkToAI Ecosystem Video

[![TalkToAI: Sovereignty Through ZeroThink and OpenZero Infrastructure](https://i.ytimg.com/vi/R52hsRdCmSM/hqdefault.jpg)](https://www.youtube.com/watch?v=R52hsRdCmSM)

A public overview of ZeroThink, OpenZero, FreeWebPanel, ZSEC, and the wider TalkToAI infrastructure. Watch it here: https://www.youtube.com/watch?v=R52hsRdCmSM

<p align="center">
  <img src="https://github.com/ResearchForumOnline/AgentZeroWordPress/blob/main/quantum-sentinel-avatar.png" alt="Quantum Sentinel Avatar" width="160">
</p>

*If you would like an AI chatbot that you can edit and re-brand without coding try our other plugin, though it is not using the advanced frameworks this Sentinel plugin is using.*
Our other WordPress plugin fully customizable plugin: 
https://github.com/ResearchForumOnline/WordpressAIchatbot

> **Modular AI assistant for WordPress — free ⚡ *Groq* by default, with effortless switches to xAI Grok, OpenAI GPT-4o/3.5 or Google Gemini, plus instant knowledge-base search.**

[![WordPress 6.x](https://img.shields.io/badge/WordPress-6.x-blue.svg)](https://wordpress.org/)
[![PHP 7.4+](https://img.shields.io/badge/PHP-7.4%2B-blue.svg)](https://www.php.net/)
![Groq API](https://img.shields.io/badge/Groq-API-green.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)

---

## 📚 Table of Contents
- [Features](#-features)
- [Architecture](#-architecture)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Quick Configuration](#-quick-configuration)
- [Usage](#-usage)
- [Hooks & Filters](#-hooks--filters)
- [FAQ](#-faq)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

| | |
|---|---|
| 🔸 **Free Groq backend** | Llama-3-70B at zero cost with sub-20 ms latency |
| 🔌 **Pluggable engines** | Swap to **xAI Grok**, **OpenAI GPT-4o / 3.5**, or **Google Gemini** in one click |
| 📖 **Knowledge-base aware** | Inject posts, pages, or custom JSON snippets so answers always match your content |
| 🛡 **Privacy controls** | Optional message logging, IP anonymisation, configurable data-retention |
| 🛠 **Developer-friendly** | 30 + hooks, PSR-12 PHP, concise vanilla-JS front-end, TypeScript typings |
| ⚡ **Lazy asset loading** | Styles and scripts enqueue only on pages containing the shortcode or block |
| 🌍 **i18n ready** | All strings wrapped in `__()` / `_e()` for translation |

---

## 🏗 Architecture

quantum-sentinel/

├── quantum-sentinel.php # Main loader & constants

├── admin/

│ └── quantum-sentinel-admin.php

├── includes/

│ ├── quantum-sentinel-core.php

│ └── class-qs-client.php # Engine abstractions (Groq, xAI, OpenAI, Gemini)

├── assets/

│ ├── quantum-sentinel-avatar.png

│ ├── qs-chat.css

│ └── qs-chat.js

└── languages/

└── quantum-sentinel.pot



*All engine endpoints extend `QS_Client_Base`, so adding a new provider is a 50-line subclass.*

---

## 📦 Requirements

| Item | Minimum |
|------|---------|
| **WordPress** | 5.8 (tested up to 6.5.0) |
| **PHP** | 7.4 (fully tested on 8.3) |
| **Browser** | Fetch & EventSource support (all modern browsers) |
| **API Key** | Free Groq key *or* xAI / OpenAI / Gemini key(s) |

---

## 🛠 Installation

```bash
# 1. Download latest release
wget https://github.com/ResearchForumOnline/AgentZeroWordPress/releases/latest/download/quantum-sentinel.zip

# 2. Upload via WP-Admin or unzip into wp-content/plugins/
unzip quantum-sentinel.zip -d wp-content/plugins/

# 3. Activate
wp plugin activate quantum-sentinel   # or use WP-Admin → Plugins

# 4. Configure
#   WP-Admin → Settings → Quantum Sentinel → enter API key(s)
⚙️ Quick Configuration
Setting	Default	Description
AI Engine	groq	Choices: groq, xai, openai, gemini
Model	llama3-70b-instruct	Engine-specific slug
Temperature	0.7	0 = strict, 1 = creative
Max Tokens	1024	Hard cap per reply
KB Source	internal	internal, posts, both
Log Retention	0	0 disables logging

🚀 Usage
Gutenberg Block
Add the “Quantum Sentinel” block.

Configure avatar side, theme (light, dark, auto) and KB subset.


[quantum_sentinel avatar="right" theme="dark" kb="product_faqs"]
PHP Helper
php
Copy
Edit
if ( function_exists( 'quantum_sentinel_render' ) ) {
    echo quantum_sentinel_render( array(
        'theme'   => 'auto',
        'avatar'  => 'left',
        'engine'  => 'openai',
        'model'   => 'gpt-4o-mini',
    ) );
}
🔧 Hooks & Filters
Hook	Context
qs_ai_request_args	Filter final request payload before HTTP call
qs_system_prompt	Replace or augment the default system prompt
qs_kb_items	Inject custom KB array programmatically
qs_after_reply	Fires after each successful response ($chat_id, $reply)
qs_user_avatar_url	Override the default avatar PNG

Full list in docs/hooks.md.

❓ FAQ
<details> <summary><strong>Is Groq really free?</strong></summary>
Yes. As of July 2025 Groq offers free access to Llama-3-70B for hobby and production use.
Check their dashboard for current rate-limits before launch day.

</details> <details> <summary><strong>Can I self-host the LLM?</strong></summary>
Absolutely. Implement a QS_Client_MyLocalLLM subclass that returns OpenAI-compatible JSON and hook it via qs_client_factory.

</details> <details> <summary><strong>Does Quantum Sentinel store user data?</strong></summary>
Message logs are off by default. When enabled, you choose retention days (0 = none) and whether IPs are anonymised. All data lives in your own DB—no SaaS middle-man.

</details>
🗺 Roadmap
 Server-Sent Events streaming

 Vision endpoints (Gemini Pro Vision, GPT-4o-Vision)

 Optional SQLite + pgvector vector store

 Full React admin panel

 Multisite (network-wide) settings

🤝 Contributing
Fork → git switch -c feature/your-feature

composer install && npm install

Run linters & tests: composer lint, npm run lint

Pull Request with a clear description — GH Actions runs PHPCS, PHPUnit & Vitest

After merge, your name appears in AUTHORS.md 🎉

📜 License
Quantum Sentinel is released under the MIT License, which is GPL-compatible.
See LICENSE for the full text.

