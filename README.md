# Ultima - AI Code Assistant

**Developed by Intellex**

Ultima is a powerful Node.js backend for AI-powered code assistance. It supports multiple AI providers (OpenAI, Claude, DeepSeek, Groq, Gemini) with features for code analysis, debugging, refactoring, and GitHub repository analysis.

> **Note**: Ultima is designed exclusively for IT and technology topics. It will only respond to questions related to programming, software development, data analysis, DevOps, and other technical subjects.

## 🚀 Quick Start

### Prerequisites
- Node.js v20.19.0+
- MySQL 8.0+

### Installation

```bash
# Install dependencies
npm install

# Configure environment
cp .env.example .env
# Edit .env with your settings

# Setup database
npm run db:setup

# Start server
npm run dev
```

Server runs at `http://localhost:3001`

## 🔑 AI Providers

| Provider | Models | Environment Variable |
|----------|--------|---------------------|
| OpenAI | gpt-4o, gpt-4o-mini | `OPENAI_API_KEY` |
| Claude | claude-sonnet-4, claude-opus-4 | `ANTHROPIC_API_KEY` |
| DeepSeek | deepseek-chat, deepseek-coder | `DEEPSEEK_API_KEY` |
| Groq | llama-3.1-70b, mixtral-8x7b | `GROQ_API_KEY` |
| Gemini | gemini-1.5-pro, gemini-1.5-flash | `GEMINI_API_KEY` |

## 🔐 Intellex Authorization

Ultima uses Intellex marketplace authorization. Users must have a valid Intellex API key to access the API.

### How It Works
1. User purchases access to Ultima on [Intellex Marketplace](https://intellex.sh)
2. User gets their API key from Intellex
3. User includes `X-Intellex-Key` header in all API requests

### Configuration
Set your agent ID in `.env`:
```env
INTELLEX_AGENT_ID=your-agent-chain-id
INTELLEX_API_URL=https://api.intellex.sh/api
```

## 📡 API Endpoints

All protected endpoints require the `X-Intellex-Key` header.

### Agent Chat
```bash
curl -X POST http://localhost:3001/api/agent/chat \
  -H "Content-Type: application/json" \
  -H "X-Intellex-Key: ix_sk_your_intellex_key" \
  -d '{
    "message": "How do I create a REST API?",
    "provider": "openai",
    "apiKey": "sk-your-key",
    "role": "backend"
  }'
```

### Code Analysis
```bash
curl -X POST http://localhost:3001/api/code/analyze \
  -H "Content-Type: application/json" \
  -H "X-Intellex-Key: ix_sk_your_intellex_key" \
  -d '{
    "code": "function add(a, b) { return a + b; }",
    "language": "javascript",
    "analysisType": "review",
    "provider": "openai",
    "apiKey": "sk-your-key"
  }'
```

### GitHub Repository Analysis
```bash
curl -X POST http://localhost:3001/api/github/analyze \
  -H "Content-Type: application/json" \
  -H "X-Intellex-Key: ix_sk_your_intellex_key" \
  -d '{
    "repoUrl": "https://github.com/user/repo",
    "provider": "openai",
    "apiKey": "sk-your-key"
  }'
```

## 🎯 Features

- **Multi-Provider AI**: OpenAI, Claude, DeepSeek, Groq, Gemini
- **Agent Roles**: Frontend, Backend, Fullstack, DevOps, Security
- **Code Analysis**: Review, Debug, Refactor, Explain, Document, Test
- **GitHub Integration**: Repository and file analysis
- **VS Code Ready**: Built-in endpoints for VS Code extension
- **Persistent History**: MySQL database for conversations
- **Learning System**: Skills and experience tracking
- **IT Topic Boundary**: Only responds to IT/programming related questions

## 📁 Project Structure

```
backend/
├── src/
│   ├── index.js           # Entry point
│   ├── config/            # Configuration
│   ├── controllers/       # Request handlers
│   ├── services/          # Business logic
│   ├── models/            # Database models
│   ├── routes/            # API routes
│   ├── middleware/        # Express middleware
│   └── utils/             # Utilities
├── database/
│   ├── schema.sql         # Database schema
│   └── setup.js           # Setup script
├── .env.example           # Environment template
└── DOCS.md               # Full documentation
```

## 📖 Documentation

See [DOCS.md](./DOCS.md) for complete API documentation.

## 🔧 Scripts

```bash
npm start        # Production server
npm run dev      # Development with hot reload
npm run db:setup # Initialize database
npm test         # Run tests
```

## 📄 License

MIT

---

**Ultima** - Developed with care by **Intellex**
