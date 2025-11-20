# AI Chat UI for Ollama

A modern, responsive chat interface for AI conversations using local Large Language Models like Ollama.

![App Screenshot](.github/screenshot.avif)

## Features

- 🎨 Modern UI with Light/Dark themes
- 📱 Responsive design & PWA support
- 🔄 Real-time streaming responses
- 💾 Local chat history
- ⚡ Zero dependencies
- 🔒 Privacy-focused (all data stays local)

## Prerequisites

- Ollama installed and running
- Modern web browser (Chrome, Edge, Safari or Firefox)

## Quick Start

1. **Configure Ollama for CORS**

   Choose your operating system:

   <details>
   <summary>Windows</summary>

   ```batch
   setx OLLAMA_ORIGINS "*"
   ```
   </details>

   <details>
   <summary>MacOS</summary>

   ```bash
   launchctl setenv OLLAMA_ORIGINS "*"
   ```
   </details>

   <details>
   <summary>Linux</summary>

   ```bash
   sudo systemctl edit ollama.service
   # Add under [Service]:
   Environment="OLLAMA_ORIGINS=*"
   
   sudo systemctl daemon-reload
   sudo systemctl restart ollama
   ```
   </details>

2. Restart Ollama
3. Visit [Chat UI](https://aichatui.layx.xyz)
4. Optional: Install as PWA for desktop-like experience

> ⚠️ **Chrome Users**: Disable 'Respect the result of Private Network Access preflights' in `chrome://flags/`

## Project Structure

```
AI_Chat_UI/
├── assets/           # Static assets (images, fonts)
│   ├── css/         # Stylesheets
│   ├── js/          # JavaScript files
│   └── icons/       # App icons
├── layx/            # Core framework
│   ├── main/        # Main components
│   └── utils/       # Utility functions
└── pages/           # Static HTML pages
```

## Development

### Customization

1. **Theme Modification**
   - Edit `/layx/main/base/variable.css` for base variables
   - Edit `/layx/main/base/variable_color.css` for color schemes

2. **UI Components**
   - Main styles: `assets/css/chat_app/main.css`
   - Core logic: `assets/js/chat_app/main.js`


## Contributing

1. Fork repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## License

MIT License - See [LICENSE](LICENSE) for details

## Roadmap

- [ ] Multi-LLM support (Claude, GPT4All)
- [ ] Enhanced theme customization
- [ ] Voice input/output
- [ ] Markdown export
- [ ] Context length management
- [ ] Custom prompts library

## Support

- [Report Bug](https://github.com/yourusername/AI_Chat_UI/issues)
- [Request Feature](https://github.com/yourusername/AI_Chat_UI/issues)
