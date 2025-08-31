# Jira LLM – AI-Augmented Jira ticket management for development teams and PMs

[![Docker](https://img.shields.io/badge/Docker-ready-blue.svg)](https://www.docker.com/)
[![Jira](https://img.shields.io/badge/Jira-integrated-0052CC.svg)](https://www.atlassian.com/software/jira)
[![LLM](https://img.shields.io/badge/LLM-Ollama-green.svg)](https://ollama.com/)

> An AI-augmented jira ticket management system powered by a **locally hosted LLM** (via [Ollama](https://ollama.com/)), **micro-frontend architecture**, and **Jira API integration**.  
> Showcase project from my [portfolio repository](https://github.com/cjakabos/portfolio-web).

![](examples/2.png)



---

## ✨ Features

- **Locally Hosted LLM with Ollama**  
  Deploy and interact with a private LLM (e.g., Deepseek R1) with configurable model setup. Maintain **data privacy** while leveraging AI insights.  
  👉 [LLM integration details](#)

- **Seamless Jira API Integration**  
  Connect securely to Jira using proxy APIs to bypass CORS restrictions.  
  👉 [API integration details](#)

- **Core Ticket Management**
    - Create, update, delete, and list Jira tickets
    - Add child tickets with one click
    - Batch-generate subtasks for epics/stories
    - AI-powered ticket refinement and updates

---

## 🎥 Demo

- Create/list/update/delete tickets  
  ![](examples/0.png)

- Refine tickets with AI suggestions  
  ![](examples/5.png)  
  ![](examples/6.png)

- Batch-generate subtasks for higher-level tickets  
  ![](examples/1.png)  
  ![](examples/2.png)

---

## 🚀 Quick Start

1. **Install Docker**

2. **Get a Jira API Key**
    - [Sign up for Jira](https://www.atlassian.com/software/jira/free)
    - [Generate an API token](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)

3. **Configure Jira in [docker-compose-app.yml](./docker-compose-app.yml)**

```yaml
   #NEXT_PUBLIC_JIRA_DOMAIN: 'https://your-jira-instance.atlassian.net'
   #NEXT_PUBLIC_JIRA_API_TOKEN: 'YOUR-API-KEY'
   #NEXT_PUBLIC_JIRA_PROJECT_KEY: 'YOURPROJECTKEY' # e.g. SCRUM
   #NEXT_PUBLIC_JIRA_EMAIL: 'youremail@example.com'

```

3. **Configure Ollama model**

Note: configure Ollama model to use with LLM_MODEL in [docker-compose-app.yml](./docker-compose-app.yml), in this example it was deepseek-r1 with 1.5B parameter ([for LLM_MODEL naming convention see Ollama](https://ollama.com/library/deepseek-r1:1.5b)), good enough for local testing purposes.
```dockerfile
  ollama:
    container_name: ollama
    build:
      context: ./
      dockerfile: Dockerfile_OLLAMA
      args:
        LLM_MODEL: 'deepseek-r1:1.5b'
    ports:
      - 11434:11434
```
4. **Run the app**

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




