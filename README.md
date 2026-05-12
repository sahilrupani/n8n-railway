# n8n — Self-Hosted Workflow Automation on Railway

<!-- Replace with your actual banner image URL -->
![n8n on Railway](https://res.cloudinary.com/dh2nt6hgh/image/upload/v1758869992/n8n_self_hosted_railway_vps_instance_b4gn01.png)

**Deploy a self-hosted n8n workflow automation instance in one click.** This template runs [n8n](https://n8n.io) on Railway with a PostgreSQL database for persistent workflow storage — no data loss on redeploys, no managed cloud subscription required.

Own your automation infrastructure. Connect 400+ apps. Pay only for Railway compute, not per-task fees.

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.com/deploy/n8n-railway)

---

## What is n8n?

n8n is an open-source workflow automation platform that lets you connect apps, APIs, and services using a visual drag-and-drop editor. Unlike Zapier or Make, n8n is:

- **Self-hostable** — your data stays on your infrastructure, not theirs
- **Fair-code licensed** — free to self-host, no per-task pricing
- **Code-friendly** — write JavaScript or Python directly inside workflows when no-code isn't enough
- **AI-ready** — native LangChain integration, AI Agent nodes, and built-in vector store support

It runs 400+ integrations out of the box: Slack, Gmail, GitHub, Postgres, HTTP requests, webhooks, cron jobs, and more.

---

## What This Template Deploys

Two Railway services, pre-wired together:

- **n8n** — the workflow engine and visual editor, running on port `5678`
- **PostgreSQL** — persistent database for workflows, credentials, and execution history

All workflow data survives redeploys. No SQLite — production-grade storage from day one.

---

## Deploy in 60 Seconds

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.com/deploy/n8n-railway)

1. Click **Deploy on Railway** above
2. Set `N8N_BASIC_AUTH_USER` and `N8N_BASIC_AUTH_PASSWORD`
3. Railway provisions n8n + PostgreSQL automatically
4. Open your Railway app URL on port `5678` — the n8n editor is live

### Environment Variables

| Variable | Required | Description |
|---|---|---|
| `N8N_BASIC_AUTH_USER` | ✅ | Username to log into the n8n editor |
| `N8N_BASIC_AUTH_PASSWORD` | ✅ | Password to log into the n8n editor |
| `PORT` | Auto | Set to `5678`. Railway injects this — do not change. |
| `DB_TYPE` | Auto | Set to `postgresdb`. Pre-configured. |
| `DB_POSTGRESDB_HOST` | Auto | Injected by Railway from the PostgreSQL service. |
| `DB_POSTGRESDB_DATABASE` | Auto | Injected by Railway from the PostgreSQL service. |
| `DB_POSTGRESDB_USER` | Auto | Injected by Railway from the PostgreSQL service. |
| `DB_POSTGRESDB_PASSWORD` | Auto | Injected by Railway from the PostgreSQL service. |

> All database variables are wired automatically between the two services — you don't need to set them manually.

---

## Common Use Cases

- **AI workflow automation** — connect OpenAI, Anthropic, or Hugging Face with your internal tools using n8n's native AI Agent nodes
- **Webhook pipelines** — receive webhooks from Stripe, GitHub, or any HTTP source and trigger multi-step workflows
- **Data sync** — move data between databases, spreadsheets, CRMs, and APIs on a schedule
- **Slack and email bots** — respond to messages, route support tickets, send automated reports
- **Self-hosted Zapier replacement** — migrate existing Zapier or Make automations to your own infrastructure with no per-task fees
- **DevOps automation** — trigger deployments, open GitHub issues, post alerts to Slack on monitoring events
- **Lead enrichment** — enrich CRM records with data from LinkedIn, Clearbit, or any API automatically

---

## n8n vs. Other Workflow Automation Platforms

### n8n vs. Zapier

Zapier charges per task — as your automations scale, costs compound quickly. n8n on Railway charges for compute only, regardless of how many tasks your workflows run. n8n also supports custom JavaScript and Python inside workflow nodes, which Zapier doesn't. And n8n runs on your infrastructure — Zapier owns your data.

### n8n vs. Make (formerly Integromat)

Make is powerful but still SaaS — your data flows through their servers and you pay per operation. n8n gives you the same visual workflow editor with full self-hosting, no operation caps, and the ability to run arbitrary code inside nodes. For teams building complex, high-volume pipelines, n8n on Railway is significantly cheaper at scale.

### n8n vs. Activepieces

Activepieces is a newer open-source Zapier alternative with a cleaner UI, but a smaller integration library (200+ vs n8n's 400+). n8n has a larger community, more mature AI/LangChain integration, and a longer track record in production. For teams needing deep AI workflow support or a broad integration library, n8n is the stronger choice today.

---

## Architecture

```
Railway Project
├── n8n Service (port 5678)
│   ├── Visual workflow editor
│   ├── Webhook receiver
│   ├── Cron scheduler
│   └── 400+ integration nodes
└── PostgreSQL Service
    ├── Workflows
    ├── Credentials (encrypted)
    └── Execution history
```

---

## After Deployment

**Mount a persistent volume** at `/home/node/.n8n` to preserve custom nodes and local files across redeploys. The PostgreSQL service handles workflow data — the volume covers everything else.

**Set up a custom domain** in Railway settings to use `https://n8n.yourdomain.com` instead of the auto-generated Railway URL.

**Secure the editor** — once set up, consider removing the public endpoint if you only need webhooks accessible externally (not the editor UI).

---

## Local Development

```bash
git clone https://github.com/sahilrupani/n8n-railway
cd n8n-railway
docker build -t n8n-railway .
docker run --rm -it \
  -p 5678:5678 \
  -e N8N_BASIC_AUTH_ACTIVE=true \
  -e N8N_BASIC_AUTH_USER=admin \
  -e N8N_BASIC_AUTH_PASSWORD=changeme \
  n8n-railway
```

Open http://localhost:5678.

---

## Related Links

- [Deploy n8n on Railway](https://railway.com/deploy/n8n-railway)
- [n8n Official Website](https://n8n.io)
- [n8n Documentation](https://docs.n8n.io)
- [n8n Community Forum](https://community.n8n.io)
- [n8n GitHub Repository](https://github.com/n8n-io/n8n)
- [n8n Integrations List](https://n8n.io/integrations)
- [n8n AI & LangChain Nodes](https://docs.n8n.io/langchain/)

---

## Credits

n8n core by [n8n-io/n8n](https://github.com/n8n-io/n8n) — fair-code license (Sustainable Use License + n8n Enterprise License).