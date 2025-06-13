# Vercel AI SDK Examples

This document provides examples of using the Vercel AI SDK for `generateText`, `streamText`, `generateObject`, passing images in `generateText`, using a schema in `generateText`, and passing file content in `generateText`. These examples assume you have the AI SDK installed (`npm install ai`) and an API key for a provider like OpenAI.

## Prerequisites
- Install the AI SDK: `npm install ai`
- Set up your environment with an API key (e.g., `OPENAI_API_KEY`).
- Use TypeScript for these examples.

## 1. generateText
Generates a single text response from a prompt.

```typescript
import { generateText } from 'ai';
import { openai } from '@ai-sdk/openai';

async function main() {
  const { text } = await generateText({
    model: openai('gpt-4o'),
    prompt: 'Write a short poem about the moon.',
  });
  console.log('Generated Text:', text);
}

main();
```

**Output**: A string containing a poem about the moon.

## 2. streamText
Streams text responses in real-time, useful for interactive applications.

```typescript
import { streamText } from 'ai';
import { openai } from '@ai-sdk/openai';

async function main() {
  const result = await streamText({
    model: openai('gpt-4o'),
    prompt: 'Tell a story about a space traveler.',
  });

  for await (const textPart of result.textStream) {
    process.stdout.write(textPart);
  }
}

main();
```

**Output**: The story is printed incrementally as it’s generated.

## 3. generateObject
Generates structured JSON output based on a schema.

```typescript
import { generateObject } from 'ai';
import { openai } from '@ai-sdk/openai';
import { z } from 'zod';

const schema = z.object({
  name: z.string(),
  age: z.number(),
  role: z.enum(['explorer', 'scientist', 'engineer']),
});

async function main() {
  const { object } = await generateObject({
    model: openai('gpt-4o'),
    schema,
    prompt: 'Generate a profile for a space mission crew member.',
  });
  console.log('Generated Object:', object);
}

main();
```

**Output**: A JSON object like `{ "name": "Alex Carter", "age": 34, "role": "scientist" }`.

## 4. Passing Images in generateText
Pass images (e.g., base64-encoded) to vision-capable models like `gpt-4o`.

```typescript
import { generateText } from 'ai';
import { openai } from '@ai-sdk/openai';

async function main() {
  const imageBase64 = 'data:image/jpeg;base64,/9j/...'; // Replace with actual base64 image
  const { text } = await generateText({
    model: openai('gpt-4o'),
    prompt: 'Describe the scene in this image.',
    messages: [
      {
        role: 'user',
        content: [
          { type: 'text', text: 'Describe the scene in this image.' },
          { type: 'image', image: imageBase64 },
        ],
      },
    ],
  });
  console.log('Image Description:', text);
}

main();
```

**Note**: Replace `imageBase64` with a valid base64-encoded image string. The model processes the image and returns a text description.

## 5. Using Schema in generateText
Use a schema to structure text output (requires `experimental_generateText` for some providers).

```typescript
import { experimental_generateText } from 'ai';
import { openai } from '@ai-sdk/openai';
import { z } from 'zod';

const schema = z.object({
  title: z.string(),
  description: z.string(),
});

async function main() {
  const { text } = await experimental_generateText({
    model: openai('gpt-4o'),
    prompt: 'Generate a product description for a futuristic gadget.',
    output: { schema },
  });
  console.log('Structured Text:', JSON.parse(text));
}

main();
```

**Output**: A JSON string like `{ "title": "Quantum Widget", "description": "A cutting-edge device..." }`.

## 6. Passing Files in generateText
Pass file content (e.g., text) as part of the prompt.

```typescript
import { generateText } from 'ai';
import { openai } from '@ai-sdk/openai';
import fs from 'fs/promises';

async function main() {
  // Example: Read a text file (replace with your file path)
  const fileContent = await fs.readFile('example.txt', 'utf-8');
  const { text } = await generateText({
    model: openai('gpt-4o'),
    prompt: `Summarize the following content:\n\n${fileContent}`,
  });
  console.log('Summary:', text);
}

main();
```

**Note**: Replace