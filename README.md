# Ultima - AI Code Assistant

<p align="center">
  <strong>Your AI-powered code assistant for smarter, faster development.</strong>
</p>

<p align="center">
  <a href="https://www.intellex.sh/agent/1">Get Access on Intellex Marketplace</a> |
  <a href="#features">Features</a> |
  <a href="#api-reference">API Reference</a> |
  <a href="#getting-started">Getting Started</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-20.x-green" alt="Node.js">
  <img src="https://img.shields.io/badge/License-MIT-blue" alt="License">
  <img src="https://img.shields.io/badge/Developed%20by-Intellex-purple" alt="Intellex">
</p>

---

## Overview

**Ultima** is an advanced AI code assistant developed by **Intellex**. It provides expert-level code assistance with support for multiple AI providers, code analysis, GitHub integration, and VS Code compatibility.

Whether you need code reviews, debugging help, refactoring suggestions, or documentation generation, Ultima delivers instant, actionable guidance.

**Get access now:** [https://www.intellex.sh/agent/1](https://www.intellex.sh/agent/1)

---

## Features

| Feature | Description |
|---------|-------------|
| **Multi-Provider AI** | Choose from OpenAI, Claude, DeepSeek, Groq, or Gemini |
| **Code Analysis** | Review, debug, refactor, explain, document, and test code |
| **GitHub Integration** | Analyze repositories, files, commits, PRs, and issues |
| **VS Code Ready** | Built-in endpoints for seamless IDE integration |
| **Specialized Roles** | Frontend, Backend, Fullstack, DevOps, Security engineer personas |
| **Conversation History** | Persistent chat history for context-aware responses |
| **IT-Focused** | Specialized exclusively in programming and technology topics |

---

## Supported AI Providers

| Provider | Models |
|----------|--------|
| OpenAI | GPT-4o, GPT-4 Turbo, GPT-3.5 Turbo |
| Claude | Claude 3 Opus, Claude 3 Sonnet, Claude 3 Haiku |
| DeepSeek | DeepSeek Chat, DeepSeek Coder |
| Groq | LLaMA 3, Mixtral 8x7B |
| Gemini | Gemini Pro, Gemini 1.5 Pro |

---

## Getting Started

### 1. Get Your API Key

Purchase access to Ultima on the Intellex Marketplace:

**[https://www.intellex.sh/agent/1](https://www.intellex.sh/agent/1)**

After purchase, you'll receive your Intellex API key (`ix_sk_...`).

### 2. Make Your First Request

```bash
curl -X POST https://your-ultima-endpoint.com/api/agent/chat \
  -H "Content-Type: application/json" \
  -H "X-Intellex-Key: ix_sk_your_intellex_key" \
  -d '{
    "message": "How do I implement JWT authentication in Node.js?",
    "provider": "openai",
    "apiKey": "sk-your-openai-key",
    "role": "backend"
  }'
```

---

## Authentication

All API requests require the `X-Intellex-Key` header with your Intellex API key.

| Header | Value | Description |
|--------|-------|-------------|
| `X-Intellex-Key` | `ix_sk_...` | Your Intellex marketplace API key |
| `Content-Type` | `application/json` | Required for POST requests |

---

## API Reference

### Base URL

```
https://your-ultima-endpoint.com/api
```

### Public Endpoints

These endpoints do not require authentication:

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/health` | Health check |
| GET | `/` | API information |

### Protected Endpoints

All protected endpoints require the `X-Intellex-Key` header.

#### Agent Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/agent/info` | Get agent information |
| GET | `/agent/providers` | List available AI providers |
| GET | `/agent/roles` | List available agent roles |
| POST | `/agent/chat` | Chat with Ultima |
| POST | `/agent/chat/stream` | Stream chat responses (SSE) |
| POST | `/agent/vscode` | VS Code command execution |
| GET | `/agent/conversations` | List conversations |
| GET | `/agent/history/:id` | Get conversation history |
| DELETE | `/agent/conversations/:id` | Delete a conversation |

#### Code Analysis Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/code/analyze` | Analyze code |
| POST | `/code/analyze/file` | Analyze a file |
| GET | `/code/analysis-types` | List analysis types |
| GET | `/code/languages` | List supported languages |
| GET | `/code/snippets` | Get saved code snippets |
| POST | `/code/snippets` | Save a code snippet |

#### GitHub Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/github/analyze/repo` | Analyze a repository |
| POST | `/github/analyze/file` | Analyze a file |
| POST | `/github/analyze/directory` | Analyze a directory |
| POST | `/github/analyze/commit` | Analyze a commit |
| POST | `/github/analyze/pr` | Analyze a pull request |
| POST | `/github/analyze/issue` | Analyze an issue |
| POST | `/github/search` | Search code in a repo |
| GET | `/github/repos` | List analyzed repos |

---

## Chat API

### Request

```http
POST /api/agent/chat
Content-Type: application/json
X-Intellex-Key: ix_sk_your_key
```

#### Request Body

```json
{
  "message": "Your question here",
  "provider": "openai",
  "apiKey": "your-ai-provider-key",
  "role": "fullstack",
  "conversationId": null,
  "customInstructions": ""
}
```

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `message` | string | Yes | Your question (IT topics only) |
| `provider` | string | Yes | AI provider: `openai`, `claude`, `deepseek`, `groq`, `gemini` |
| `apiKey` | string | Yes | API key for the AI provider |
| `role` | string | No | Agent role: `frontend`, `backend`, `fullstack`, `devops`, `security` |
| `conversationId` | string | No | Continue an existing conversation |
| `customInstructions` | string | No | Additional instructions |

#### Response

```json
{
  "success": true,
  "conversationId": "conv_abc123",
  "response": "Here's how to implement JWT authentication...",
  "usage": {
    "promptTokens": 150,
    "completionTokens": 320,
    "totalTokens": 470
  },
  "metadata": {
    "provider": "openai",
    "model": "gpt-4o",
    "role": "backend",
    "messageId": "msg_xyz789"
  }
}
```

---

## Code Analysis API

### Request

```http
POST /api/code/analyze
Content-Type: application/json
X-Intellex-Key: ix_sk_your_key
```

#### Request Body

```json
{
  "code": "function add(a, b) { return a + b; }",
  "language": "javascript",
  "analysisType": "review",
  "provider": "openai",
  "apiKey": "your-ai-provider-key",
  "context": "Optional context about the code"
}
```

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `code` | string | Yes | Code to analyze |
| `language` | string | Yes | Programming language |
| `analysisType` | string | Yes | Type of analysis |
| `provider` | string | Yes | AI provider |
| `apiKey` | string | Yes | API key for the provider |
| `context` | string | No | Additional context |

#### Analysis Types

| Type | Description |
|------|-------------|
| `review` | Comprehensive code review |
| `debug` | Find and fix bugs |
| `refactor` | Suggest improvements |
| `explain` | Explain how the code works |
| `document` | Generate documentation |
| `test` | Generate unit tests |
| `security` | Security audit |

---

## GitHub Analysis API

### Analyze Repository

```http
POST /api/github/analyze/repo
Content-Type: application/json
X-Intellex-Key: ix_sk_your_key
```

```json
{
  "owner": "facebook",
  "repo": "react",
  "provider": "openai",
  "apiKey": "your-ai-provider-key",
  "githubToken": "ghp_optional_token"
}
```

### Analyze File

```http
POST /api/github/analyze/file
```

```json
{
  "owner": "expressjs",
  "repo": "express",
  "path": "lib/router/index.js",
  "analysisType": "review",
  "provider": "openai",
  "apiKey": "your-ai-provider-key"
}
```

---

## VS Code Integration

Ultima provides a dedicated endpoint for VS Code extension integration.

### Request

```http
POST /api/agent/vscode
Content-Type: application/json
X-Intellex-Key: ix_sk_your_key
```

```json
{
  "command": "explain",
  "selection": "const result = useMemo(() => compute(a, b), [a, b]);",
  "fileContext": {
    "fileName": "App.tsx",
    "language": "typescript",
    "startLine": 15,
    "endLine": 15
  },
  "provider": "openai",
  "apiKey": "your-ai-provider-key"
}
```

### Available Commands

| Command | Description |
|---------|-------------|
| `explain` | Explain selected code |
| `refactor` | Suggest refactoring |
| `debug` | Debug issues in code |
| `document` | Generate documentation |
| `test` | Generate unit tests |
| `optimize` | Optimize for performance |

---

## Agent Roles

| Role | Expertise |
|------|-----------|
| `frontend` | React, Vue, Angular, CSS, UI/UX, accessibility |
| `backend` | Node.js, Python, databases, APIs, microservices |
| `fullstack` | End-to-end development, architecture |
| `devops` | Docker, Kubernetes, CI/CD, cloud infrastructure |
| `security` | Security audits, vulnerability assessment, encryption |

---

## Error Handling

### Error Response Format

```json
{
  "error": "Error message",
  "code": "ERROR_CODE"
}
```

### Common Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `MISSING_INTELLEX_KEY` | 401 | X-Intellex-Key header not provided |
| `INVALID_INTELLEX_KEY` | 401 | Invalid API key |
| `ACCESS_DENIED` | 403 | No access to this agent |
| `EXPIRED_ACCESS` | 403 | Subscription expired |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests |

---

## Rate Limits

Rate limits are managed through your Intellex subscription. Check your plan details at [intellex.sh](https://www.intellex.sh).

---

## Topic Boundaries

Ultima is specialized in IT and technology topics only:

**Supported Topics:**
- Programming and software development
- Web and mobile development
- DevOps and cloud infrastructure
- Databases and data engineering
- Data science and machine learning
- Cybersecurity
- System design and architecture
- Technical documentation

**Out of Scope:**
- General knowledge unrelated to technology
- Personal advice, entertainment, sports
- Medical, legal, or financial advice

---

## Examples

### Chat Example

```bash
curl -X POST https://your-endpoint.com/api/agent/chat \
  -H "Content-Type: application/json" \
  -H "X-Intellex-Key: ix_sk_your_key" \
  -d '{
    "message": "Explain the difference between REST and GraphQL",
    "provider": "openai",
    "apiKey": "sk-your-key",
    "role": "backend"
  }'
```

### Code Review Example

```bash
curl -X POST https://your-endpoint.com/api/code/analyze \
  -H "Content-Type: application/json" \
  -H "X-Intellex-Key: ix_sk_your_key" \
  -d '{
    "code": "async function getData() { const res = await fetch(url); return res.json(); }",
    "language": "javascript",
    "analysisType": "review",
    "provider": "openai",
    "apiKey": "sk-your-key"
  }'
```

### GitHub Repo Analysis Example

```bash
curl -X POST https://your-endpoint.com/api/github/analyze/repo \
  -H "Content-Type: application/json" \
  -H "X-Intellex-Key: ix_sk_your_key" \
  -d '{
    "owner": "vercel",
    "repo": "next.js",
    "provider": "openai",
    "apiKey": "sk-your-key"
  }'
```

---

## Support

For support and feature requests:

- **Intellex Marketplace:** [https://www.intellex.sh/agent/1](https://www.intellex.sh/agent/1)
- **Issues:** Open an issue in this repository

---

## License

MIT License

---

<p align="center">
  <strong>Ultima</strong> - Developed with care by <strong>Intellex</strong>
</p>

<p align="center">
  <a href="https://www.intellex.sh/agent/1">Get Started</a>
</p>
