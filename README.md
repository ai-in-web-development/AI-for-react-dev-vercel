<style>
* {
  box-sizing: border-box;
}

/* Create three equal columns that floats next to each other */
.column {
  float: left;
  width: 33.33%;
  padding: 10px;
  height: 300px; /* Should be removed. Only for demonstration */
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
</style>

## AI for React Developers
### A Deep Dive into the Vercel's AI SDK
- Tech Stack: Next.js 15.2.4 with React 19, TailwindCSS, Vercel AI SDK, multiple provider SDKs (@ai-sdk/openai, @ai-sdk/google, @ai-sdk/groq), React-specific hooks (@ai-sdk/react)
- Link to [original slides](https://milindmishra.com/slide/ai-for-react-developers):  .
- [Link to original GitHub repository](https://github.com/thatbeautifuldream/ai-for-react-developers)
- (Based on presentation at [React meetup #88](https://github.com/kurtzace/diary-2025/tree/main/seminars/reactmeetup88) on April 12th, 2025) - speech by [Milind Mishra](https://www.linkedin.com/in/mishramilind/), Product Engineer, Merlin AI

---
## Why AI in React Development?
*   AI is **already here** in web development, not just the future.
*   Knowledge of AI tooling is **critical for future-proofing careers** for React developers.
*   Easy for React/Next Developers who are not very comfortable with Python notebooks
--
## Introducing the Vercel AI SDK
*   An **approachable on-ramp** for anyone comfortable with React.
*   Makes it **easier to incorporate the new paradigms of generative AI and streaming user interfaces** in a React app.
*   Provides a **powerful and streamlined way to integrate various AI capabilities** into React applications.
*   Leverages the latest web technologies.
---
## Example Project: AI for React Developers
*   A cutting-edge Next.js application showcasing **AI integration patterns and best practices** for modern React development.
*   Demonstrates various **AI-powered features and tools**.
*   [Associated GitHub repository](https://github.com/thatbeautifuldream/ai-for-react-developers)
--
## Example Project: Tech Stack
*   **Framework:** Next.js 15.2.4 with React 19
*   **Styling:** TailwindCSS
*   **AI Integration:**
    *   **Vercel AI SDK** (`ai` package)
    *   Multiple provider SDKs (`@ai-sdk/openai`, `@ai-sdk/google`, `@ai-sdk/groq`)
    *   React-specific hooks (`@ai-sdk/react`)
*   **UI Components:** Radix UI primitives, Framer Motion, Lucide React
*   **Type Safety:** TypeScript with Zod for schema validation
---
## Example Project: Key Features
### ** Multi-Model Support**
*   **OpenAI:** GPT-3.5 Turbo, GPT-4, GPT-4 Turbo
*   **Google AI:** Gemini Pro, Gemini 1.5 Pro, Gemini Pro Vision, Gemini Pro Vision for Image Generation
*   **Groq:** Llama2-70B, Mixtral-8x7B
--
## Example Project: Advanced AI Capabilities
*   **Text Generation:** Basic completion for all supported models.
*   **Streaming Responses:** Real-time text streaming for interactive UIs.
*   **Structured Data:** Stream typed objects with schema validation.
*   **Tool Calling:** Function calling with OpenAI models.
*   **Image Generation:** Create images using Gemini Pro Vision.
--
## Example Project: Vercel AI SDK Specifics
*   **Streaming UI components** with React suspense.
*   **Type-safe schema validation** with Zod.
*   **Standardized API interfaces** across providers.
*   **Edge runtime support** for optimal performance.
--
## Simple server
```
import { openai } from "@ai-sdk/openai";
import { streamText } from "ai";
export async function POST(req) {
  const { messages } = await req.json();
  const result = await streamText({ 
    model: openai("gpt-4o-mini"), messages });
  return result.toAIStreamResponse();}
```
--
## Simple client
```
import { readStreamableValue } from "ai/rsc";
        onClick={async () => {
          const { output } = await generate({inputText});
          for await (const delta of readStreamableValue(
            output
          )) {
            setMyState(
              (currentGeneration) => `${currentGeneration}${delta}`
            );
          } }}
```
--
## Zod json generate
```
      const { partialObjectStream } = await streamObject({
      model: openai("gpt-4o-mini"),
      system: "You generate fake data for three people",
      prompt: input,
      schema: z.object({ people: z.array(
          z.object({ name: z.string().describe("name of a fake person"),
            address: z.string().describe("US address format"),
            age: z.number()
          }) ) }) });
    for await (const partialObject of partialObjectStream) {
      stream.update(partialObject);
    } stream.done();
```
--
## Use chat
```
import { useChat } from "ai/react";
  const {
    messages, input, handleInputChange, handleSubmit, isLoading
  } = useChat();

<form onSubmit={handleSubmit}>
<input  value={input} placeholder="..." onChange={handleInputChange} disabled={isLoading} />
```
---
## Example Project: API Structure
Comprehensive API implementation showcasing different AI capabilities.

```json
{ openai: {
    generateText: '/api/openai/generate-text', streamText: '/api/openai/stream-text',
    streamObject: '/api/openai/stream-object', toolCalling: '/api/openai/tool-calling' },
  google: {...similar},
  groq: { generateText, streamText, streamObject  }
}
```
*Example API routes from `thatbeautifuldream/ai-for-react-developers` repository, demonstrating different AI capabilities by provider.*
---
## Related Resource: LinkedIn Learning Course
*   "AI for React Developers" in LinkedIn Learning by **Eve Porcello**.
*   Focuses on understanding the **Vercel AI SDK** as an approachable on-ramp.
*   Helps React developers build **streaming interfaces** with JavaScript/TypeScript.
*   Covers streams, generative AI functions, components, & generating structured data.
*   [Associated GitHub repository](https://github.com/LinkedInLearning/ai-for-react-developers-5917130):
*   Repository has branches corresponding to course videos.
---
## Key Takeaways
*   AI is rapidly becoming **essential for web developers**, especially in the React ecosystem.
*   The **Vercel AI SDK** simplifies integrating generative AI and streaming UIs into React/Next.js apps.
*   The SDK supports **multiple AI providers** and structured data/tool calling.
*   Leveraging - Vercel AI SDK is **key to building smarter, faster, and more fun applications** right in the browser.
```