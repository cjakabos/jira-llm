# Jira LLM – AI-Augmented Jira ticket management for development teams and PMs
<p align="center">
  <a href="https://www.docker.com/">
    <img src="https://img.shields.io/badge/Docker-ready-blue?logo=docker" alt="Docker Ready">
  </a>
  <a href="https://www.atlassian.com/software/jira">
    <img src="https://img.shields.io/badge/Jira-integrated-0052CC?logo=jira" alt="Jira Integrated">
  </a>
  <a href="https://ollama.com/">
    <img src="https://img.shields.io/badge/LLM-Ollama-green?logo=opensourceinitiative" alt="Ollama">
  </a>
  <a href="https://github.com/cjakabos/jira-llm/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/cjakabos/jira-llm" alt="License">
  </a>
  <a href="https://github.com/cjakabos/jira-llm/commits/main">
    <img src="https://img.shields.io/github/last-commit/cjakabos/jira-llm" alt="Last Commit">
  </a>
  <a href="https://github.com/cjakabos/jira-llm/pulls">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome">
  </a>
</p>

<p align="center">
  <a href="https://github.com/cjakabos/jira-llm/stargazers">
    <img src="https://img.shields.io/github/stars/cjakabos/jira-llm?style=social" alt="Stars">
  </a>
  <a href="https://github.com/cjakabos/jira-llm/network/members">
    <img src="https://img.shields.io/github/forks/cjakabos/jira-llm?style=social" alt="Forks">
  </a>
</p>

> An AI-augmented jira ticket management system powered by a **locally hosted LLM** (via [Ollama](https://ollama.com/)), **micro-frontend architecture**, and **Jira API integration**.  
> Showcase project from my [portfolio repository](https://github.com/cjakabos/portfolio-web).

![](examples/2.png)



---

## ✨ Features

- **Locally Hosted LLM with Ollama**  
  Deploy and interact with a private LLM (e.g., Deepseek R1) with configurable model setup. Maintain **data privacy** while leveraging AI insights.  
  👉 [LLM integration details](#4-configure-ollama-model)

- **Seamless Jira API Integration**  
  Connect securely to Jira using proxy APIs to bypass CORS restrictions.  
  👉 [API integration details](#3-configure-jira-in-docker-compose-appymldocker-compose-appyml)

- **Core Ticket Management**
    - Create, update, delete, and list Jira tickets
    - Add child tickets with one click
    - Batch-generate subtasks for epics/stories
    - AI-powered ticket refinement and updates

---

## 🎥 Demo

- Create/list/update/delete tickets and turn on AI mode
  ![](examples/0.png)

- Refine tickets with AI suggestions: choose chat with the ticket and/or including parent tickets
  ![](examples/5.png)  
- Edit suggestions before update
  ![](examples/6.png)

- Batch-generate subtasks for higher-level tickets: choose how many tickets to generate
  ![](examples/1.png) 
  and select/edit the proposals
  ![](examples/2.png)

---

## 🚀 Quick Start

Minimum system requirements: 15GB free disk space, 16GB RAM. Scale it accordingly, when choosing a larger LLM model.

## 1. **Install Docker**
Install Docker on your system:
#### macOS:
- Download Docker Desktop from [docker.com](https://www.docker.com/products/docker-desktop)
- Or install via Homebrew:
```bash
brew install docker
brew install docker-compose
```
#### Linux (Ubuntu/Debian):
```bash
sudo apt install docker.io docker-compose
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
```
#### Windows:
- Download Docker Desktop from [docker.com](https://www.docker.com/products/docker-desktop)
- Connected to the same network as your Docker host

## 2. **Get a Jira API Key**
  [Sign up for Jira](https://www.atlassian.com/software/jira/free)

  [Generate an API token](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)

## 3. **Configure Jira in [docker-compose-app.yml](./docker-compose-app.yml)**

```yaml
   #NEXT_PUBLIC_JIRA_DOMAIN: 'https://your-jira-instance.atlassian.net'
   #NEXT_PUBLIC_JIRA_API_TOKEN: 'YOUR-API-KEY'
   #NEXT_PUBLIC_JIRA_PROJECT_KEY: 'YOURPROJECTKEY' # e.g. SCRUM
   #NEXT_PUBLIC_JIRA_EMAIL: 'youremail@example.com'
   #NEXT_PUBLIC_LLM_MODEL = 'deepseek-r1:1.5b'

```

## 4. **Configure Ollama model**

Note: configure Ollama model to use with NEXT_PUBLIC_LLM_MODEL in [docker-compose-app.yml](./docker-compose-app.yml), in this example it was deepseek-r1 with 1.5B parameter ([for NEXT_PUBLIC_LLM_MODEL naming convention see Ollama](https://ollama.com/library/deepseek-r1:1.5b)), good enough for local testing purposes.
```dockerfile
  ollama:
    container_name: ollama
    build:
      context: ./
      dockerfile: Dockerfile_OLLAMA
      args:
        NEXT_PUBLIC_LLM_MODEL: 'deepseek-r1:1.5b'
    ports:
      - 11434:11434
```
## 5. **Run the app**

this will setup the Jira proxy, Jira frontend and LLM backend:
```bash
docker-compose -f docker-compose-app.yml up -d
```

4. **That's it!** Go to http://localhost:5003 to start to talk with your Jira tickets.

## 👨‍💻 Local Development
1. Web-Proxy API to avoid CORS issues with Jira. Listens on port 8500. For local run see [instructions](./backend/web-proxy/README.md)
2. Local Jira frontend: see [instructions](./frontend/jira/README.md)
3. For Ollama use the Docker configuration, either chat with the model via the Jira frontend or use command line:
```bash
curl http://localhost:11434/api/generate -d '{                              
  "model": "deepseek-r1:1.5b",
  "prompt": "Why is the sky blue?"
}'
```
📄 License
MIT License © 2025 Csaba Jakabos

  Feel free to fork, modify, and contribute! Please star if you like the project!




