# Docker Compose Collection
This repository contains a curated collection of Docker Compose files I actively use in my own environments.

People regularly ask what I run, how it’s configured, and whether I’m willing to share it. This repo is the answer - versioned, documented, and public.

Each service lives in its own directory, with its own README that explains:

- What the service does
- Why it exists here
- Anything non-obvious about configuration or behavior
- Where to find the upstream project

No screenshots. No mystery ZIP files. No “DM me for details.”
 - Each stack is self-contained.
- There is no global Compose file and no hidden orchestration layer.
- If a project depends on external infrastructure, it is documented in that project’s README.

## What This Repo Is
- Practical Compose files used beyond “hello world”
- Opinionated defaults shaped by long-term use
- Designed for homelabs, test labs, and environments that tend to become permanent
- Intended to be copied, adapted, and improved

This is working material, not marketing collateral.

## What This Repo Is Not
- A turnkey product
- A guarantee of production readiness
- A substitute for understanding what you’re deploying
- A promise that every service will fit every environment

If you deploy these files unchanged and expect magic, you will be disappointed.
If you read them, understand them, and adapt them, you’ll be fine.

## Security and Secrets
This repository intentionally excludes:
- `.env` files
- Secrets and API keys
- Certificates and private keys
- Runtime data
- Backups
- Logs

You are expected to supply sensitive values locally.
.env.example files exist to show structure and intent - not safe defaults.
If something authenticates, encrypts, or grants access, it does not belong in Git.



## Assumptions and Expectations

These Compose files assume:
- Docker Compose v2
- Comfort with Docker networking and volumes
- Basic Linux hygiene
- A willingness to read the README before running docker compose up

Some projects may expect existing infrastructure such as:

- Reverse proxies
- External Docker networks
- DNS, authentication, or storage services
- Those expectations are documented per project.

## Change and Stability
Services change. Images move. Patterns improve. Compose files in this repository may evolve as:
- Upstream projects change
- Better configurations emerge
- Hard-earned lessons are learned

Breaking changes can happen.
Each project’s README should be treated as the authoritative reference for that stack.

## License and Use
Unless stated otherwise:
- Use these files
- Fork them
- Modify them
- Learn from them

Just don’t repackage them as a silver bullet or imply endorsement.

## Final Note
This repository exists to reduce friction, not eliminate responsibility.
If it helps you build something better, it’s doing its job.

