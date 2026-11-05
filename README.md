# SPACE SHOOTER ODYSSEY

An original browser-based space shooter where players pilot spaceships, battle enemy waves and bosses, complete missions, collect rewards, and upgrade their fleet.

## Features

- Five campaign sectors and progressive missions
- Real-time 2D combat powered by Phaser 3
- Spaceship selection and upgrades
- Eight gameplay power-ups
- Player progression, achievements, and daily missions
- Wallet, rewards, and optional rewarded-ad flow
- Player profiles, leaderboard, and settings
- Admin tools for economy management and analytics

## Tech Stack

| Layer          | Technology                          |
| -------------- | ----------------------------------- |
| Frontend       | React, Vite, JavaScript, CSS3       |
| Game Engine    | Phaser 3                            |
| Backend        | Java, Spring Boot, REST API         |
| Authentication | Spring Security, JWT                |
| Database       | PostgreSQL (Supabase)               |
| ORM            | Spring Data JPA, Hibernate          |
| Build Tool     | Maven                               |
| Testing        | Postman                             |
| Deployment     | Vercel (frontend), Render (backend) |

## Project Structure

```text
space-shooter-odyssey/
├── client/       # React application and Phaser game
├── server/       # Spring Boot REST API
├── postman/      # API test collection
└── docs/         # Project documentation
```

## Getting Started

### Requirements

- Node.js and npm
- Java JDK
- Maven
- PostgreSQL database (or Supabase project)

### Frontend

```bash
cd client
npm install
npm run dev
```

### Backend

```bash
cd server
./mvnw spring-boot:run
```

Configure the required environment variables before starting the application. Refer to the `.env.example` files when available.

## Environment Configuration

**Frontend (`client/.env`)**

```env
VITE_GAME_NAME=SPACE SHOOTER ODYSSEY
VITE_API_URL=http://localhost:8080/api
```

**Backend (`server/.env`)**

Configure the PostgreSQL connection, JWT secret, server port, game name, and allowed frontend origin using the backend environment configuration.

Never commit real credentials, API keys, or secret environment files.

## Documentation

Detailed project documentation is maintained separately:

- `PROJECT_CONTEXT.md` — goals, features, and architecture
- `DATABASE_SCHEMA.md` — database design and relationships
- `DESIGN_SYSTEM.md` — visual design and UI guidelines
- `TYPOGRAPHY_FONT_SPECIFICATIONS.md` — fonts and typography
- `SYSTEM_FLOW.md` — application flows and API overview

## Deployment

- Frontend: Vercel
- Backend: Render
- Database: Supabase PostgreSQL

Set production environment variables and configure the frontend origin in the backend CORS settings before deployment.

## Project Status

This repository is intended to contain the complete frontend, backend, game assets, API tests, and project documentation. Features should be considered complete only when implemented and tested.

---

**SPACE SHOOTER ODYSSEY** — Explore the sectors. Defeat the enemy fleets. Upgrade your ship.
