# 🤖 OnChain AI with Motoko

This repository provides an example of how to build an **on-chain AI agent** on the Internet Computer (IC) using **Motoko** and the **LLM Canister** developed by the DFINITY Foundation. This project demonstrates how to deploy a Motoko canister that interacts with the LLM Canister to generate text responses on-chain using the `mo:llm` library.

## ✨ Overview

- **Leverages the LLM Canister**: The DFINITY Foundation’s LLM Canister makes it easy to integrate AI-driven text generation into your IC projects.  
- **Motoko-Based**: This project uses Motoko, the native language for the Internet Computer, ensuring straightforward deployment and canister interactions.  
- **Simple Implementation**: The agent uses the `mo:llm` library to send user prompts to the LLM Canister and return responses.
- **Expandable**: Developers can modify the prompt logic or enhance interactions by customizing the response processing.

---

## 🚀 Getting Started

### 1. Prerequisites

1. **DFX SDK**: Make sure you have the [DFX SDK](https://internetcomputer.org/docs/current/developer-docs/build/install-upgrade-remove) installed.
2. **Node.js & pnpm**: Install [Node.js](https://nodejs.org/) and [pnpm](https://pnpm.io/installation) to manage frontend dependencies.
3. **Ollama (Optional)**: If you want to test locally with a model served on your machine, [install Ollama](https://ollama.com/) and follow the instructions in the “Local Testing with Ollama” section below.

### 2. Clone & Install

```bash
git clone https://github.com/pt-icp-hub/ICP-AI-Hackathon-OnChain-Motoko.git
cd ICP-AI-Hackathon-OnChain-Motoko

# Install frontend dependencies
cd src/frontend
pnpm install
cd ../..
```

---

### 3. Local Testing with Ollama (Optional)

If you prefer using a local LLM instead of the on-chain LLM Canister for testing, you can run [Ollama](https://ollama.com/):

1. **Run Ollama Server**  
   ```bash
   ollama serve
   # Expected to start listening on port 11434
   ```
2. **Download a Model** (e.g., llama2)  
   ```bash
   ollama run llama2:7b
   # This will download the model; you can terminate once the model loads.
   ```

> **Note**: You can modify the code in this repo to point your requests to Ollama locally rather than the LLM Canister. This is useful for offline experimentation.

---

### 4. Deploy to the Internet Computer

1. **Start the Local Replica**  
   ```bash
   dfx start --clean
   ```
2. **Deploy Canisters**  
   ```bash
   dfx deploy
   ```
3. **Access the Frontend**  
   After deployment, you’ll see a URL similar to:
   ```
   http://127.0.0.1:8080/?canisterId=<FRONTEND_CANISTER_ID>
   ```
   However, due to browser CORS policies, it’s recommended to access the agent via:
   ```
   http://<FRONTEND_CANISTER_ID>.localhost:8080
   ```

---

## 🏗 Project Structure

```
ICP-AI-Hackathon-OnChain-Motoko/
├── src
│   ├── backend
│   │   └── main.mo         # Core Motoko code interacting with the LLM Canister
│   ├── frontend
│   │   ├── assets
│   │   ├── dist
│   │   ├── src
│   │   ├── index.html
│   │   └── package.json    # Frontend package management
├── dfx.json               # DFX configuration
└── README.md              # You are here
```

- **`main.mo`**: Contains the logic to interact with the LLM Canister via the `mo:llm` library.  
- **`frontend`**: Basic web interface to send prompts and display responses.  
- **`dfx.json`**: Configures canisters for local testing and deployment.

---

## 🛠 Core Functionality

The agent uses the `mo:llm` library for interacting with the LLM Canister:

```motoko
import LLM "mo:llm";

actor {
  public func prompt(prompt : Text) : async Text {
    await LLM.prompt(#Llama3_1_8B, prompt)
  };

  public func chat(messages: [LLM.ChatMessage]) : async Text {
    await LLM.chat(#Llama3_1_8B, messages)
  }
};
```

- **`prompt` Function**: Sends a single prompt to the LLM Canister and returns the AI-generated response.
- **`chat` Function**: Sends a sequence of chat messages, allowing multi-turn interactions.

---

## 🔍 Going Further: Using LLM Canister as a Tooling Agent

For those interested in building specialized AI agents on the Internet Computer, check out the **ICP Lookup Agent**, an example of using the LLM Canister for specific tasks like looking up ICP balances. This project showcases how to structure an AI agent to specialize in a particular function. 

This is where you can unleash your creativity, imagining different tools that AI could use. Whether it’s financial data retrieval, smart contract interactions, or other domain-specific utilities, the possibilities are endless!

🔗 **Check out the example here:** [ICP Lookup Agent Motoko](https://github.com/dfinity/llm/tree/main/examples/icp-lookup-agent-motoko)

---

## 🤝 Contributing

We welcome contributions! Feel free to open issues or pull requests to improve this template. Join the [IC Developer Community](https://forum.dfinity.org/) for discussions, updates, and collaboration.

---

## 📚 Learn More

- [LLM Canister Introduction Post](https://forum.dfinity.org/t/introducing-the-llm-canister-deploy-ai-agents-with-a-few-lines-of-code/41424)  
- [Internet Computer Documentation](https://internetcomputer.org/docs/home)  
- [Motoko Language Reference](https://internetcomputer.org/docs/current/developer-docs/build/languages/motoko)  

---

**Happy hacking!** Build your own on-chain AI agent and explore the limitless potential of AI on the Internet Computer. If you have any questions or need help, feel free to reach out via the forum or our community channels.
