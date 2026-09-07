# JanAwaaz — Voice of the People 🗣️

JanAwaaz is a full-stack civic engagement platform that lets citizens report, track, and resolve local infrastructure problems — broken roads, garbage, water leaks, power outages, and more — while giving government authorities a dedicated dashboard to act on them. It was built as a submission for **India Innovates (Municipal Corporation of Delhi)**, where it was ranked among the top teams out of 25,000+ nationwide entries.

**🔗 Live demo:** https://janawaaz.onrender.com/home

## Why JanAwaaz

Civic issues usually get lost between a citizen's complaint and the right municipal department ever seeing it. JanAwaaz closes that loop with a single platform where issues are geotagged, publicly visible, upvoted by the community, and routed to verified authorities who are accountable for resolving them — with the whole lifecycle tracked from report to resolution.

## Features

### For Citizens
- Report infrastructure issues with photos and precise geolocation
- Upvote issues to surface the most urgent problems in a neighborhood
- Comment and engage in discussion on active issues
- Follow issues and get real-time notifications as their status changes
- Track full resolution history and progress updates
- View all reported issues on an interactive district/city map
- Start and support petitions on recurring civic problems
- Rate authorities on how issues were handled

### For Authorities
- A dedicated dashboard to accept, triage, and update assigned issues
- Identity verification workflow (Aadhaar-based) before authority accounts are activated
- Post official responses and resolution updates
- Leaderboard ranking authorities by resolution speed and volume, computed via MongoDB aggregation pipelines
- Analytics on issue volume, response time, and resolution rate by area

### For Admins
- Moderate reports, users, and comments
- Review and approve/reject authority applications
- Full audit log of moderation and administrative actions

## Tech Stack

**Frontend:** HTML5, CSS3, vanilla JavaScript (no framework) — MapLibre + OpenStreetMap for maps, Chart.js for analytics visualizations

**Backend:** Node.js, Express.js, MongoDB Atlas with Mongoose ODM

**Real-time & Auth:** Socket.io for live notifications and status updates, JWT-based authentication with bcrypt password hashing, role-based access control (citizen / authority / admin)

**Media & Data:** Cloudinary for image uploads, Multer for handling multipart uploads, XLSX for bulk authority data import

## Architecture Highlights

- **20 Mongoose models** covering issues, users, authorities, petitions, ratings, notifications, audit logs, and identity verification — reflecting a genuinely multi-role, multi-workflow system rather than a single-entity CRUD app
- **Role-gated middleware** (`authenticate`, `isAuthority`, `isAdmin`) protecting routes by JWT-verified role
- **Optimized MongoDB aggregation pipelines** for the leaderboard and analytics endpoints, computing per-authority resolution time and rankings server-side instead of in application code
- **Socket.io integration** for pushing live updates (new comments, status changes, notifications) to connected clients without polling
- **Connection pooling** and lean/selective queries tuned for lower latency under load
- **Aadhaar-based identity verification pipeline** (OTP + hashed ID storage) gating authority account activation

## Project Structure

```
JanAwaaz/
├── server/
│   ├── server.js              # Express app entry point, Socket.io init
│   ├── config/                # DB, Cloudinary config
│   ├── middleware/             # Auth (JWT, role checks)
│   ├── models/                 # 20 Mongoose schemas
│   ├── routes/                 # REST API endpoints (auth, issues, authority, leaderboard, analytics, etc.)
│   ├── utils/                   # Socket.io setup, Aadhaar verification helpers
│   └── scripts/ / seed.js      # Data seeding and import scripts
├── public/                     # HTML pages (feed, issue detail, dashboards, admin, profile)
├── css/                         # Stylesheets per page/feature
├── js/                           # Client-side logic per page/feature
└── scripts/                     # Performance test scripts
```

## Getting Started

```bash
# Clone the repo
git clone <repo-url>
cd JanAwaaz

# Install dependencies
npm install

# Configure environment variables (create a .env file)
MONGODB_URI=<your MongoDB Atlas URI>
JWT_SECRET=<your JWT secret>
CLOUDINARY_URL=<your Cloudinary URL>
CLIENT_URL=<your frontend URL, for production CORS>

# Seed sample data (optional)
npm run seed

# Run in development
npm run dev

# Run in production
npm start
```

The app serves on `http://localhost:5000` by default (or the port defined in your environment).

## Achievements

- 🏆 **Finalist, India Innovates** — Municipal Corporation of Delhi, ranked among top teams out of 25,000+ nationwide entries

