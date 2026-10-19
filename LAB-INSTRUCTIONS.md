# ResideFix - Docker lab demonstration

The `residefix-final.zip` nested file from the original upload is deliberately NOT included. No original `.env` secrets or `node_modules` are included.

## Before the lab

Install Docker Desktop (Docker Compose V2) and Git. Start Docker Desktop and verify it is running.

## Publish files to an EXISTING GitHub repository

Copy the project files including `compose.yaml`, the two Dockerfiles and `.dockerignore` files into the existing repository at their matching paths (do not overwrite unrelated work). Commit and push:

```powershell
git add .
git commit -m "Add ResideFix Docker Compose lab setup"
git push origin main
```

If your branch is not named main, use `git push` instead.

## On booked lab computer

```powershell
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
Copy-Item .env.example .env
notepad .env
```

Replace JWT_SECRET value with a long unique random string and save. Then:

```powershell
docker compose up --build -d
docker compose ps
```

Open http://localhost:5173/login (or http://localhost:5173 if redirected). Backend health check: http://localhost:5000/ . Registration is needed before you can sign in to the fresh empty MongoDB database.

If you made the frontend-only Docker image rather than using Compose, login requests won't work without backend and database. Docker Desktop and enough disk/RAM plus image download access are necessary.

## Troubleshooting

```powershell
docker compose logs -f backend
docker compose logs -f frontend
docker compose down
```

Avoid `docker compose down -v` unless you intentionally want to erase MongoDB data.

This sample starts the Vite development server for classroom demonstration, not a hardened production deployment. The `src/api.js` URL is localhost:5000, which is correct when the web browser and Docker containers run on the same lab computer.
