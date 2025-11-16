---
name: ai-integration
description: Build AI-powered features with Claude, GPT-4, and Gemini
---

# AI Integration - Build AI-Powered Apps

Add AI capabilities to any application with streaming, function calling, and RAG.

## Quick Setup

```bash
# Install AI SDKs
npm install openai @anthropic-ai/sdk @google/generative-ai
npm install @vercel/ai # Unified streaming interface
```

## Available AI Features

### 1. Chat Interface
```typescript
// Streaming chat with any model
import { streamText } from '@vercel/ai';

const response = await streamText({
  model: 'gpt-4-turbo', // or 'claude-3', 'gemini-pro'
  messages: [...],
  temperature: 0.7,
});
```

### 2. Function Calling
```typescript
// Let AI call your functions
const tools = {
  getWeather: z.object({
    city: z.string()
  }),
  searchDatabase: z.object({
    query: z.string()
  })
};

const response = await ai.chat({
  tools,
  toolChoice: 'auto'
});
```

### 3. RAG (Retrieval-Augmented Generation)
```typescript
// Build ChatGPT for your docs
import { PineconeClient } from '@pinecone-database/pinecone';

// 1. Embed documents
const embeddings = await openai.embeddings.create({
  input: documents,
  model: 'text-embedding-3-small'
});

// 2. Store in vector DB
await pinecone.upsert(embeddings);

// 3. Query with context
const context = await pinecone.query(userQuestion);
const response = await ai.chat({
  messages: [
    { role: 'system', content: `Context: ${context}` },
    { role: 'user', content: userQuestion }
  ]
});
```

### 4. Image Generation
```typescript
// Generate images with DALL-E 3
const image = await openai.images.generate({
  model: 'dall-e-3',
  prompt: 'A serene landscape...',
  size: '1024x1024',
  quality: 'hd'
});
```

### 5. Voice & Speech
```typescript
// Text-to-speech
const audio = await openai.audio.speech.create({
  model: 'tts-1',
  voice: 'nova',
  input: 'Hello world!'
});

// Speech-to-text
const transcription = await openai.audio.transcriptions.create({
  file: audioFile,
  model: 'whisper-1'
});
```

## Complete Examples

### ChatGPT Clone in 5 Minutes
```typescript
// app/api/chat/route.ts
import { streamText } from '@vercel/ai';
import { openai } from '@ai-sdk/openai';

export async function POST(req: Request) {
  const { messages } = await req.json();
  
  const result = await streamText({
    model: openai('gpt-4-turbo'),
    messages,
  });
  
  return result.toAIStreamResponse();
}

// app/page.tsx
'use client';
import { useChat } from '@vercel/ai/react';

export default function Chat() {
  const { messages, input, handleInputChange, handleSubmit } = useChat();
  
  return (
    <div>
      {messages.map(m => (
        <div key={m.id}>
          {m.role}: {m.content}
        </div>
      ))}
      <form onSubmit={handleSubmit}>
        <input value={input} onChange={handleInputChange} />
        <button>Send</button>
      </form>
    </div>
  );
}
```

### AI Agent with Tools
```typescript
const agent = createAgent({
  model: 'claude-3-sonnet',
  tools: {
    searchWeb: async ({ query }) => {
      // Search implementation
    },
    analyzeData: async ({ data }) => {
      // Analysis logic
    },
    sendEmail: async ({ to, subject, body }) => {
      // Email logic
    }
  }
});

const result = await agent.run('Research competitors and email me a report');
```

## Best Practices

1. **Always stream responses** for better UX
2. **Implement rate limiting** to control costs
3. **Cache embeddings** to reduce API calls
4. **Use temperature 0** for factual tasks
5. **Log all completions** for debugging
6. **Implement fallbacks** between models

## Cost Optimization

```typescript
// Use smaller models for simple tasks
const model = complexity === 'high' 
  ? 'gpt-4-turbo'  // $0.01/1k tokens
  : 'gpt-3.5-turbo'; // $0.001/1k tokens

// Cache common queries
const cached = await redis.get(queryHash);
if (cached) return cached;
```

## Environment Variables
```bash
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
GOOGLE_AI_API_KEY=...
PINECONE_API_KEY=...
```

## Ready-to-Use Patterns

Say any of these to get started:
- "Build a ChatGPT clone with streaming"
- "Add AI search to my docs"
- "Create an AI customer support bot"
- "Generate product descriptions with AI"
- "Build an AI code reviewer"