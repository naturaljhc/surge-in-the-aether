# Surge In The Aether

A web-based deck builder and game simulator for **Final Fantasy Trading Card Game (FFTCG)**. Build or import decks to match up against other players or a bot using custom decks.

## Features

- **Deck Builder**
  - Main Deck: Exactly 50 cards (max 3 copies per card)
  - Limit Break Deck: Exactly 8 cards (special subset)
  - Format validation (Standard, L3, L6, Title)
  
- **Game Modes** (Planned)
  - vs Player (Casual sandbox, future Elo/matchmaking)
  - vs Computer (AI opponents with increasing difficulty)
  
- **Draft Modes** (Planned)
  - Sealed: Build from 108-card pool (9 booster packs)
  - Moogle Market (Name Pending): Limited currency draft with shop mechanics
  
- **Cosmetics & Customization**
  - Custom card backs for main and LB decks
  - Playmat selection
  - Future: Foil cards and alternative art (cosmetic currency)
  
- **User Authentication**
  - Email/password sign-up
  - Username creation with profanity filtering
  - Persistent deck storage via Supabase

## 🛠️ Tech Stack

- **Frontend**: React 19 + TypeScript
- **Build Tool**: Vite (with HMR)
- **Styling**: Tailwind CSS 4 + Framer Motion (animations)
- **Database**: Supabase (PostgreSQL + Real-time)
- **Routing**: React Router 7
- **Auth**: Supabase Auth (email/password)

## 📁 Project Structure

```
src/
├── App.tsx             # Router & auth guards
└── main.tsx            # React entry point

public/
├── assets/
│   ├── cards/          # Card art images
│   └── card-backs/     # Cosmetic card backs
├── data/
│   └── card_data.json  # Card metadata (sets, rarities, etc.)
└── fonts/              # Custom fonts (FinalF)

docs/
└── prd.md              # Detailed game specification
```

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- npm or yarn
- Supabase account

### Installation

1. **Clone the repository**
   ```bash
   git clone <repo>
   cd fftcg-sim
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create `.env.local` at the project root:
   ```
   VITE_SUPABASE_URL=https://<project-ref>.supabase.co
   VITE_SUPABASE_ANON_KEY=<your-publishable-key>
   ```
   
   Get these from your Supabase project dashboard.

4. **Set up the database**

5. **Start the dev server**
   ```bash
   npm run dev
   ```
   
   Open [http://localhost:5173](http://localhost:5173)

## 🔐 Authentication Flow

## 🔄 State Management

## 📦 Database Schema

## 🎯 Roadmap

## 🐛 Troubleshooting

## 🤝 Contributing

This is a personal learning project. Feel free to suggest improvements!

## 📄 License

MIT License — see [LICENSE](LICENSE) file for details.