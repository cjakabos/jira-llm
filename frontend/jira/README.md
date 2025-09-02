Copy .env.sample as .env and edit:

```bash
NEXT_PUBLIC_JIRA_DOMAIN = 'https://xxxx.atlassian.net'
NEXT_PUBLIC_JIRA_API_TOKEN = Y3NhYmFqYWthYm-------YOUR-API-KEY------SDA9REUzRjY4N0M=
NEXT_PUBLIC_JIRA_PROJECT_KEY: 'yourjiraprojectkey'
NEXT_PUBLIC_JIRA_EMAIL: 'youremail'
NEXT_PUBLIC_LLM_MODEL: 'deepseek-r1:1.5b'
```

Run locally:
```bash
npm install
npm run dev
```

Go to http://localhost:5003

