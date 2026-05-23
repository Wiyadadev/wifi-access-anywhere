# WiFi Vault

A personal WiFi password manager web app — save, search, and share your WiFi credentials securely from anywhere.

## Features

- **Save WiFi Networks** — store network name, password, location, security type, and notes
- **Instant Search** — find any network in seconds from the dashboard
- **Password Reveal & Copy** — toggle visibility or copy password to clipboard with one click
- **QR Code Sharing** — generate a scannable QR code so guests can join instantly (iOS & Android)
- **PIN Lock** — protect the vault with a 4-digit PIN and auto-lockout after failed attempts
- **Import / Export CSV** — back up all your networks or transfer to another device
- **WiFi Password Guide** — built-in guide on how to find WiFi passwords on iPhone, Android, Windows, and Mac

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| Backend | Node.js, Express 5, TypeScript |
| Database | PostgreSQL, Drizzle ORM |
| API Contract | OpenAPI 3.1, Orval (code generation) |
| Validation | Zod |
| QR Code | qrcode.react |
| Monorepo | pnpm workspaces |

## Screenshots

> Dashboard — search, stats, and recent networks at a glance

> Network Detail — blurred password, reveal toggle, copy button, and QR code sharing

## Getting Started

### Prerequisites

- Node.js 20+
- pnpm 9+
- PostgreSQL database

### Installation

```bash
# Clone the repository
git clone https://github.com/<your-username>/wifi-vault.git
cd wifi-vault

# Install dependencies
pnpm install

# Set environment variables
cp .env.example .env
# Edit .env and add your DATABASE_URL

# Push the database schema
pnpm --filter @workspace/db run push

# Start the API server
pnpm --filter @workspace/api-server run dev

# Start the frontend (in a new terminal)
pnpm --filter @workspace/wifi-vault run dev
```

The app will be available at `http://localhost:5173`

### Environment Variables

| Variable | Description |
|----------|-------------|
| `DATABASE_URL` | PostgreSQL connection string |
| `SESSION_SECRET` | Secret key for sessions |

## Project Structure

```
wifi-vault/
├── artifacts/
│   ├── api-server/      # Express API server
│   └── wifi-vault/      # React frontend
├── lib/
│   ├── api-client-react/ # Generated React Query hooks
│   ├── api-spec/         # OpenAPI specification
│   ├── api-zod/          # Generated Zod schemas
│   └── db/               # Drizzle ORM schema & client
└── scripts/              # Utility scripts
```

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/networks` | List all networks (supports `?search=`) |
| POST | `/api/networks` | Create a new network |
| GET | `/api/networks/:id` | Get a single network |
| PATCH | `/api/networks/:id` | Update a network |
| DELETE | `/api/networks/:id` | Delete a network |
| GET | `/api/networks/stats` | Get summary statistics |

## Security Notes

- Passwords are stored in PostgreSQL — use a private, secured database
- PIN lock is client-side (localStorage) — intended as a convenience lock, not a cryptographic security layer
- Deploy behind HTTPS in production

## Live Demo

[View Live App](https://wifi-vault.replit.app) *(deploy your own instance)*

## License

MIT
