---
description: Complete guide for developing in the Soc Ops workspace
---

# Soc Ops Workspace Instructions

## ✅ Mandatory Development Checklist

Before committing or opening a PR:
- [ ] **Lint** — Code follows project standards
- [ ] **Build** — `cd socops && ./mvnw clean package` succeeds
- [ ] **Test** — `cd socops && ./mvnw test` passes (100%)

---

Welcome to **Soc Ops**—a Spring Boot social bingo game for in-person mixers.

## Quick Start

**Prerequisites:** Java 21 JDK, Maven 3.9+ (included via `./mvnw`)

```bash
cd socops && ./mvnw spring-boot:run
# App runs at http://localhost:8080
```

## Project Structure

```
socops/                              # Spring Boot app
├── src/main/java/com/socops/
│   ├── SocOpsApplication.java       # Entry point
│   ├── service/BoardAssembler.java  # Game logic
│   ├── web/BingoRestController.java # REST endpoints
│   ├── model/                       # Domain objects
│   └── data/IcebreakerPrompts.java  # Question pool
├── src/main/resources/
│   ├── templates/game.html          # Main UI
│   └── static/css/app.css           # Utilities
└── src/test/                        # Unit tests

.github/instructions/
├── workspace.instructions.md (this file)
├── css-utilities.instructions.md
└── frontend-design.instructions.md

workshop/                           # 5-part curriculum
├── 00-overview.md
├── 01-setup.md
├── 02-design.md
├── 03-quiz-master.md
└── 04-multi-agent.md
```

## Commands

| Task | Command |
|------|---------|
| Run dev server | `cd socops && ./mvnw spring-boot:run` |
| Build JAR | `cd socops && ./mvnw clean package` |
| Run tests | `cd socops && ./mvnw test` |
| Clean | `cd socops && ./mvnw clean` |

## Architecture

**Game Flow:** Lobby → Game (5×5 grid) → Winner (5 in a row)

**API:**
- `GET /` — Main page
- `GET /api/board` — Questions & board state
- `POST /api/mark` — Toggle cell

**Key Classes:**
- `BoardAssembler` — Generation, win detection
- `BingoRestController` — HTTP endpoints
- `BingoCell` — Grid cell model
- `PlayPhase` — State enum

## Development Tasks

### Add Questions
Edit `IcebreakerPrompts.java` and add strings to `PROMPTS` list.

### Style UI
Use CSS utilities from `app.css` (no external dependencies). See [css-utilities.instructions.md](.github/instructions/css-utilities.instructions.md).

### Extend Backend
- Game rules: `BoardAssembler.java`
- Endpoints: `BingoRestController.java`
- Data: `model/` directory

### Enhance Frontend
See [frontend-design.instructions.md](.github/instructions/frontend-design.instructions.md) for design patterns.

## Testing

```bash
cd socops && ./mvnw test
```

Main test class: `BoardAssemblerTests.java`

## Learning

1. [00-overview.md](../../workshop/00-overview.md) — Project overview
2. [01-setup.md](../../workshop/01-setup.md) — Environment ✅ Done
3. [02-design.md](../../workshop/02-design.md) — Frontend design
4. [03-quiz-master.md](../../workshop/03-quiz-master.md) — Custom quizzes
5. [04-multi-agent.md](../../workshop/04-multi-agent.md) — Advanced patterns

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Port 8080 in use | `lsof -i :8080` → `kill <PID>` |
| Build fails | `cd socops && ./mvnw clean install` |
| Tests fail | `cd socops && ./mvnw test -X` (debug) |
| Java mismatch | `java -version` must return 21.x.x |

---

**Happy coding!** 🎲
