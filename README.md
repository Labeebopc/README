# :bar_chart: – Developer Notes
This document outlines the tools, optimization practices, and full folder structure used in an app. It helps ensure consistency and scalability while developing and maintaining the project.
---
## :hammer_and_wrench: Tech Stack
| Layer       | Tool                      |
|-------------|---------------------------|
| Frontend    | React + TypeScript + Tailwind CSS |
| Backend     | Node.js + Express (JavaScript)    |
| Database    | MongoDB (via Mongoose)    |
| State Mgmt  | Zustand / Redux (Frontend)|
| Charts      | Recharts                  |
| UI Kit      | ShadCN UI + Lucide Icons  |
| Deployment  | Vercel (Frontend) / Railway/Render (Backend) |
| Others      | ESLint + Prettier, GitHub Actions (optional) |
---
## :white_check_mark: Optimization Checklist
### :small_blue_diamond: Frontend (React + TypeScript)
- [x] Lazy load routes/modals (`React.lazy`)
- [x] Debounce search & filter inputs
- [x] Memoize expensive components with `React.memo`/`useMemo`
- [x] Use Zustand or Redux for predictable state management
- [x] Responsive layout (mobile-first with Tailwind)
- [x] Skeleton loaders/spinners for async content
- [x] Use pagination & virtual scroll for large datasets
- [x] Type-safe API with shared interfaces
### :small_blue_diamond: Backend (Node.js + MongoDB)
- [x] Use indexes on `date`, `symbol`, `userId`, `status`
- [x] Paginated endpoints (`limit`, `skip`)
- [x] Separate service layer (analytics, reports)
- [x] Secure headers, rate limiting, and input validation
- [x] Use environment configs (`.env`)
- [x] Logging with Winston or Pino (optional)
- [x] API versioning (future-proofing)
- [x] Clean modular route/controllers/services
---
## :white_check_mark: Shared Optimization
### :small_orange_diamond: API Design
- RESTful standards with proper pagination, filtering, status codes.
- Avoid over-fetching: use precise query params.
- Compress responses using gzip.
### :small_orange_diamond: Database Hygiene
- Regular archiving of old trades.
- Scheduled cleanup of unused records (e.g., temp import files).
---
## :card_index_dividers: Folder Structure
```bash
project-folder/
│
├── backend/                      # Node.js (JavaScript)
│   ├── config/                   # DB connection and env
│   ├── controllers/              # Business logic
│   ├── middleware/               # Auth, error handling
│   ├── models/                   # Mongoose models (User.js, Trade.js)
│   ├── routes/                   # API route handlers
│   ├── services/                 # Core logic (analytics, CSV import)
│   ├── utils/                    # Reusable functions
│   ├── app.js                    # Express app entry
│   ├── server.js                 # Server start script
│   └── .env                      # Environment variables
│
├── frontend/                     # React + Tailwind (TypeScript)
│   ├── public/                   # Static files
│   ├── src/
│   │   ├── assets/               # Logos, icons, images
│   │   ├── components/           # Shared UI components (Button, Table)
│   │   ├── features/             # Domain features (Trades, Filters, Reports)
│   │   ├── hooks/                # Custom React hooks (e.g., useAuth)
│   │   ├── pages/                # Pages (Dashboard, Reports, AddTrade)
│   │   ├── services/             # API clients (axios/fetch)
│   │   ├── store/                # Zustand/Redux store slices
│   │   ├── types/                # Global TS interfaces/types
│   │   ├── utils/                # Formatters, calculations
│   │   ├── App.tsx               # Root App component
│   │   └── main.tsx              # ReactDOM render entry point
│   ├── tailwind.config.ts
│   ├── tsconfig.json
│   ├── vite.config.ts
│   ├── index.html
│   └── package.json
│
├── shared/                       # (Optional) Shared helpers/types
│   ├── constants/
│   ├── helpers/
│   └── types/
│
├── .gitignore
├── README.md
└── docker-compose.yml            # (Optional) MongoDB + backend containers
