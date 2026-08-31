# Kannamma - Maternal Health Voice Guardian

<div align="center">

![GitHub repo](https://img.shields.io/badge/GitHub-kannamma--vision2047hackathon---181717?logo=github)
![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python)
![Flask](https://img.shields.io/badge/Flask-3.x-000000?logo=flask)
![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript)
![Twilio](https://img.shields.io/badge/Twilio-IVR-ef3b2d?logo=twilio)
![Hackathon](https://img.shields.io/badge/Track-Vision2047-8a2be2)

</div>

> “A mother doesn’t need an app — she just needs a voice that remembers.”

Kannamma is a maternal health support platform that helps expecting mothers and ASHA workers stay connected through AI-assisted voice reminders, health tracking, and care coordination. The system uses an IVR-based calling flow to deliver weekly reminders in Tamil/Telugu, surface health risks, and connect mothers to the right care support quickly.

## Overview

Kannamma combines:

- an automated voice-first reminder system for pregnancy care
- a dashboard for ASHA workers and healthcare staff
- structured health tracking for mothers
- appointment and medicine coordination
- PHC inventory visibility and follow-up management

This project is designed for rural maternal care scenarios where timely voice reminders and low-friction communication can reduce missed checkups and improve support access.

## Key Features

- IVR voice calls in Tamil/Telugu for reminders and follow-ups
- Weekly health and medication check-ins for pregnant mothers
- ASHA worker dashboard for mother tracking and outreach
- Appointment and visit tracking
- PHC stock and vaccine monitoring
- Flagged mother workflow for urgent follow-up
- Call logs and engagement history

## Solution Architecture

```text
Mother / Community
       |
       v
IVR + Twilio Integration
       |
       v
Flask Backend API
       |
       +--> SQLite/PostgreSQL data layer
       +--> ASHA dashboard and workflow APIs
       +--> Health, appointment, and stock services
       |
       v
React + TypeScript Frontend
```

## Quick Start

### Backend

```bash
cd backend
python setup.py
python app.py
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

### Windows helpers

```powershell
cd backend
.
un.bat
# or
.
un.ps1
```

## Default Access

After running the backend setup, the system includes a sample ASHA login:

- ASHA ID: `ASHA001`
- Password: `password123`

## Project Structure

```text
kannamma/
├── backend/                 # Flask API service
├── frontend/                # React + TypeScript dashboard
├── database/                # SQL schema and migration support
├── README.md                # Project overview
├── PROJECT_STRUCTURE.md     # Repo structure details
├── START_HERE.md            # Launch guide
├── API_STATUS.md            # API status notes
├── TESTING_GUIDE.md         # Testing instructions
├── TWILIO_SETUP.md          # Twilio setup docs
├── NGROK_SETUP.md           # Local webhook setup
├── start-demo.bat           # Demo launch helper
└── test_api.ps1             # API testing helper
```

## Documentation

- [START_HERE.md](./START_HERE.md) — recommended starting point
- [PROJECT_STRUCTURE.md](./PROJECT_STRUCTURE.md) — file organization
- [TESTING_GUIDE.md](./TESTING_GUIDE.md) — validation workflow
- [TWILIO_SETUP.md](./TWILIO_SETUP.md) — Twilio configuration
- [NGROK_SETUP.md](./NGROK_SETUP.md) — local webhook testing
- [backend/README.md](./backend/README.md) — backend API documentation

## Tech Stack

### Backend
- Flask
- Python
- SQLAlchemy
- Flask-JWT-Extended
- Twilio API

### Frontend
- React
- TypeScript
- Vite
- Tailwind CSS

## Use Cases

1. Weekly maternal health reminders delivered by voice
2. ANC visit tracking and follow-up reminders
3. ASHA worker visibility into high-risk mothers
4. PHC medicine and vaccine stock tracking
5. Faster escalation for mothers needing intervention

## Contributing

1. Fork the repository
2. Create a feature branch
3. Implement your improvement
4. Open a pull request

## License

This project is developed as part of a hackathon initiative for maternal health innovation.

## Acknowledgements

Built to support community health workers and mothers in underserved areas, especially in rural and semi-urban maternal care settings.

---

Made with ❤️ for mothers, ASHA workers, and healthier communities.

