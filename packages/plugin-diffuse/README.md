# @elizaos/plugin-diffuse

Allows making provable requests to LLM APIs using diffuse system.

## Installation

```bash
pnpm add @elizaos/plugin-diffuse
```

## Configuration

Add the following environment variables to your `.env` file:

```env
DIFFUSE_APP_ID=your_app_id
DIFFUSE_APP_SECRET=your_app_secret
DIFFUSE_ENABLED=true
```

## Usage

```typescript
import { DiffusePlugin } from "@elizaos/plugin-diffuse";

// Initialize the plugin
const diffusePlugin = new DiffusePlugin(runtime, {
    appId: process.env.DIFFUSE_APP_ID,
    appSecret: process.env.DIFFUSE_APP_SECRET,
});

// request data
const options: VerifiableInferenceOptions = {
    // Optional: Override the default endpoint
    endpoint: "https://custom-api.example.com",
    // Optional: Add custom headers
    headers: {
        "X-Custom-Header": "value",
    },
    // Optional: Provider-specific options
    providerOptions: {
        temperature: 0.7,
    },
};

const result = await diffusePlugin.generateText(
    "What is Node.js?",
    "gpt-4",
    options
);

console.log("Response:", result.text);
console.log("Proof:", result.proof);
```

## Response Format

The adapter returns a `Proof` object containing:

```typescript
{
    proofType: string; // sgx_quote or risc0 or sp1
    zkProof: string;   // proof
    text: string;      // server response
}
```

## License

MIT