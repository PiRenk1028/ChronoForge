# ChronoForge
a small, full-stack game


ChronoForge: Full-Stack Development Roadmap
🧩 Phase 1: Planning & Setup (Days 1–3)
🎯 Goals:

Define the game’s data model & architecture.

Set up a clean dev environment.

Establish Git version control and folder structure.

✅ Tasks:

Create your repo (chronoforge).

Initialize Git + GitHub.

Add README.md describing the concept and roadmap.

Set up backend environment:

Python 3.12+

Install FastAPI, uvicorn, and PyMySQL (or SQLAlchemy if desired).

Create /backend folder.

Add entrypoint main.py with “Hello World” FastAPI endpoint.

Run: uvicorn main:app --reload

Set up MySQL database:

Local or Docker MySQL instance.

Create database chronoforge_db.

Manually create simple test table and confirm connection.

Plan the architecture:

/backend/

main.py → app entry

routes/ → API endpoints

models/ → database models

schemas/ → Pydantic validation

services/ → business logic

auth/ → JWT + password hashing

/frontend/

(empty for now, to be created later)

📘 Deliverable:

FastAPI “Hello World” running locally and connected to MySQL.

⚙️ Phase 2: Core API Foundations (Days 4–10)
🎯 Goals:

Build the backbone API to manage users, authentication, and game entities.

✅ Tasks:

Implement authentication:

POST /register → hash password (bcrypt)

POST /login → issue JWT token

Middleware to protect endpoints using JWT

Create database tables:

users, monsters, dungeons, relics, combat_logs

Create endpoints for CRUD:

GET /dungeons → fetch available dungeons

GET /monsters/:id → monster details

GET /user/me → get current user info

POST /relics/forge → forge a new relic (for testing)

Implement data models (example):

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    username = Column(String(50), unique=True)
    password_hash = Column(String(128))
    xp = Column(Integer, default=0)
    level = Column(Integer, default=1)


📘 Deliverable:

Secure REST API with authentication and working CRUD endpoints.

Able to register, login, and fetch dungeons.

⚔️ Phase 3: Combat System Prototype (Days 11–20)
🎯 Goals:

Implement the “Chrono Energy” battle mechanic and backend combat logic.

✅ Tasks:

Design combat logic (in /services/combat_engine.py):

Define enemy actions (AI logic or random strategy).

Define player actions (attack, defend, alter_time).

Define turn resolution and damage formula.

Return results and updated player state.

Example pseudo-code:

def resolve_turn(player, monster, actions):
    player_damage = actions["attack"] * player.attack_power
    monster_damage = monster.attack - actions["defend"] * player.defense
    time_effect = actions["alter_time"] * 0.2
    next_turn_bonus = player_damage * (1 + time_effect)
    return {"damage_to_enemy": player_damage, "damage_to_player": monster_damage, "bonus": next_turn_bonus}


API endpoints:

POST /combat/start → begin encounter (load monster)

POST /combat/turn → resolve a turn, update states

POST /combat/end → store combat log + update XP

Database logging:

Save each completed battle’s results in combat_logs.

📘 Deliverable:

Fully functional combat engine accessible through API.

JSON-based turn resolution working via Postman.

🎨 Phase 4: Front-End MVP (Days 21–30)
🎯 Goals:

Build the player interface to interact with the API.

✅ Tasks:

Initialize /frontend project

Option 1: Vanilla JS + HTML + CSS

Option 2: React (recommended for portfolio)

Pages:

Login / Register page

Dashboard (shows player stats)

Dungeon selector

Combat screen (attack/defend/alter-time buttons)

Integrate API:

Use Fetch API or Axios to call endpoints.

Handle JWT storage and authentication.

Create simple animations or feedback:

Health bars

Turn summaries

Relic inventory screen

📘 Deliverable:

Playable local version of the game where you can log in and fight monsters.

💾 Phase 5: Persistence & Progression (Days 31–40)
🎯 Goals:

Add long-term player progression, items, and a save system.

✅ Tasks:

Implement XP and leveling:

Gain XP after each battle.

Auto-increase stats when leveling up.

Relic system:

Forge relics with earned time shards.

Each relic modifies stats or combat rules.

Inventory management:

Add DB relation: user_relics (many-to-many)

GET /inventory → list player relics

Update UI to display progress.

📘 Deliverable:

Persistent player growth system + visible relic inventory.

🌐 Phase 6: Polish & Deployment (Days 41–50)
🎯 Goals:

Turn your local project into a public, portfolio-grade app.

✅ Tasks:

Testing

Write unit tests for combat engine and API routes.

Integration tests for user auth flow.

Deployment

Containerize with Docker (backend + MySQL).

Deploy backend to Render or AWS Lightsail.

Deploy frontend to Vercel or Netlify.

Use environment variables for secrets.

Documentation

Clean README.md with:

Overview

Screenshots

Tech stack

Installation instructions

API reference

Design notes

📘 Deliverable:

Fully deployed full-stack RPG.

Documented and demo-ready portfolio project.
