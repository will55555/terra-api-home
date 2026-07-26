# Terra API Home — Setup Guide

This is the root orchestration repository for the Terra Inc ecosystem. It coordinates:
- **terra-api** — Backend API (Spring Boot, Java 21)
- **terra-api-fe** — Frontend Dashboard (React 19)
- **terra-jenkins** — Jenkins CI/CD Infrastructure

## One-Time Setup (First Machine)

```bash
# Clone this repo first
git clone https://github.com/will55555/terra-api-home.git
cd terra-api-home

# Clone the three child repos as siblings
git clone https://github.com/will55555/terra-api.git
git clone https://github.com/will55555/terra-api-fe.git
git clone https://github.com/will55555/terra-jenkins.git

# Checkout active branches
cd terra-api && git checkout phase-6-cicd && cd ..
cd terra-api-fe && git checkout main && cd ..
```

## On Every Machine (or after pulling updates)

```bash
# From terra-api-home/ folder
docker-compose up -d
```

## Services Running

- **Backend API:** http://localhost:8081
- **Actuator/Health:** http://localhost:8082/actuator/health
- **Jenkins:** http://localhost:8090
- **PostgreSQL:** localhost:5433 (terra / 5945)
- **Redis:** localhost:6379

## Important Rules

**DO:**
- Commit orchestration changes (docker-compose.yml, docker.env, README.md) to this repo
- Commit app code changes (Java, React) to the child repos (terra-api, terra-api-fe)
- Pull updates from this repo on every machine to stay in sync

**DON'T:**
- Create docker-compose files in child repos (they'll be rejected by .gitignore)
- Commit app code to this repo
- Manually edit docker-compose.yml on different machines (pull from git instead)

## Troubleshooting

**Services won't start?**
- Ensure you're in the terra-api-home folder (not a child repo)
- Check `docker ps` for orphaned containers: `docker-compose down --remove-orphans`
- Verify docker.env exists and has correct values

**Changes to docker-compose not taking effect?**
- Stop services: `docker-compose down`
- Restart: `docker-compose up -d`

**Drift between machines?**
- Always pull this repo on every machine: `git pull origin main`
- Never commit docker-compose changes to child repos
- Use `git status` to verify clean working tree before pulling

---

See terra-api/DEV_LOG.md for detailed Docker infrastructure documentation.
