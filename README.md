# WeMind Backend Engineer Challenge: Learning Tracker API

Welcome to the **WeMind Backend Engineering Challenge**! In this task, you'll build a backend API that helps users track their learning habits, similar to how we support teens and young adults in building healthy, consistent learning behaviors through our platform. We’re excited to see how you structure your solution, think through edge cases, and approach real-world product challenges.

---

## 🚀 Getting Started

### 💻 Tech Stack & Requirements

- **Backend Language**: TypeScript (NestJS preferred)
- **Database**: Any relational database (SQLite for simplicity, PostgreSQL for production-level design)
- **API Type**: RESTful API
- **Optional Tools**:
  - Docker for containerization
  - ORM for easier database interaction (Prisma Preferred)

### 📦 Submission Guidelines

[Submission Form](https://forms.gle/Zydo8vLhaK6EENNt9)

- Host your code on a **public GitHub repository** and share the link, **OR** send a `.zip` file of your project.
- Include a `README.md` file with:
  - Setup instructions (install, run migrations, start server)
  - How to test the API
  - Assumptions and design decisions
  - Answers to the bonus product questions

**You're allowed to make assumptions about the product—just be sure to document your reasoning clearly.*

---

## 🧠 Background

At **WeMind**, we’re building a platform that helps **teens** and **young adults** manage their learning goals through short sessions (like micro-learning). **Users log their daily progress** in different topics (e.g., "Mindfulness", "Math", "Communication").

The platform rewards **consistency**, and our product team is experimenting with **streaks**, **summaries**, and **progress insights** to encourage daily engagement.

You're brought in to rebuild the core learning tracker backend with **scalability** and **reliability** in mind.

---

## 🎯 Objectives

Build a RESTful API that allows:

- Creating users
- Recording learning sessions
- Listing sessions
- Getting total duration per topic (summary)
- Calculating current streak of consecutive learning days
- Insights to be used in user dashboards and sent via email or push notifications **(Optional)**

---

## 🗃️ API Requirements
*You can update, add, or do anything with the models. The models listed below is only the basic.*

### User Model
```json
{
  "id": "uuid",
  "name": "string",
  "email": "string"
}
```

### LearningSession Model
```json
{
  "id": "uuid",
  "userId": "uuid",
  "topic": "string",
  "duration": 25,
  "date": "YYYY-MM-DD",
  "notes": "optional"
}
```

### Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| POST   | `/users` | Create a user |
| POST   | `/users/:userId/sessions` | Add a session |
| GET    | `/users/:userId/sessions` | List sessions |
| GET    | `/users/:userId/summary?from=YYYY-MM-DD&to=YYYY-MM-DD` | Duration summary per topic |
| GET    | `/users/:userId/streak` | Get current streak |
| GET (Optional)    | `/users/:userId/insights` | Get insight for dashboard |

---

## 📘 Example Scenario

Declan logs 4 sessions:

| Date       | Topic         | Duration |
|------------|---------------|----------|
| 2025-04-01 | Focus         | 30 min   |
| 2025-04-02 | Mindfulness   | 20 min   |
| 2025-04-03 | Communication | 25 min   |
| 2025-04-05 | Focus         | 15 min   |

### Sample Requests & Responses

#### POST `/users`
```json
{
  "name": "Declan Rice",
  "email": "d.rice@example.com"
}
```

#### POST `/users/uuid/sessions`
```json
{
  "topic": "Focus",
  "duration": 30,
  "date": "2025-04-01",
  "notes": "Struggled to stay focused today."
}
```

#### GET `/users/uuid/sessions`
```json
[
  { "topic": "Focus", "duration": 30, "date": "2025-04-01" },
  { "topic": "Mindfulness", "duration": 20, "date": "2025-04-02" },
  { "topic": "Communication", "duration": 25, "date": "2025-04-03" },
  { "topic": "Focus", "duration": 15, "date": "2025-04-05" }
]
```

#### GET `/users/uuid/summary?from=2025-04-01&to=2025-04-05`
```json
[
  { "topic": "Focus", "totalDuration": 45 },
  { "topic": "Mindfulness", "totalDuration": 20 },
  { "topic": "Communication", "totalDuration": 25 }
]
```

#### GET `/users/uuid/streak`
```json
{
  "currentStreak": 1,
  "lastActiveDate": "2025-04-05"
}
```

#### GET `/users/uuid/insights` (Optional)
```json
{
  "currentStreak": 1,
  "longestStreak": 3,
  "lastActiveDate": "2025-04-05",
  "mostStudiedTopic": "Focus",
  "totalMinutesThisWeek": 90,
  "averageDailyMinutes": 22.5,
  "recommendation": "You're doing great! Try not to miss tomorrow to keep your streak going."
}
```

### How this is calculated (from the example data):

- **Current streak**: 1 day (2025-04-05)
- **Longest streak**: 3 days (2025-04-01 to 2025-04-03)
- **Most studied topic**: "Focus" (30 + 15 = 45 mins)
- **Total minutes this week**: 90
- **Average daily minutes**: 90 ÷ 4 days = 22.5

---

## 🧠 Bonus Product Questions

Answer these in `README.md`:

1. If this platform scales to 100k users:
   - How would you handle streak calculation without slowing the system?
   - Would you compute it live or cache it? Why?

2. If a product manager says, “We want the streak calculation to be real-time, but only during daytime hours,” how would you design that?

3. Suppose you notice duplicate learning sessions in the DB — how would you prevent or resolve this?

---

## ✅ What We'll Evaluate

| Category           | Criteria                                       |
|--------------------|------------------------------------------------|
| API Design         | RESTful, well-structured, correct status codes |
| Code Quality       | Readable, modular, tested                      |
| Problem Solving    | Handles streaks, summaries, duplicates         |
| Product Thinking   | Smart assumptions, scalable design             |
| Bonus Edge Handling| Consistency, queuing, latency aware            |
