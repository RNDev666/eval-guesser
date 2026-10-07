# Eval Guesser - Chess Position Evaluation Training

A chess training application that helps players improve their positional understanding by guessing computer evaluations of chess positions. Built with Next.js 15, React 19, and TypeScript.

## 🎮 Features

### Game Modes

#### Classic Mode
- Guess the exact evaluation of chess positions
- Interactive evaluation bar that always shows your current guess
- Get scored based on accuracy with generous thresholds
- Track streaks (within 1.5 pawns counts as correct)
- Auto-progression to next puzzle after 2 seconds
- Theme-based puzzle selection

#### Analysis Board
- Full-featured chess analysis with Stockfish engine
- Real-time position evaluation
- Top 3 engine variations displayed
- Interactive board with complete move freedom
- Move history navigation
- Keyboard shortcuts for navigation

### Core Features

- **🎯 Evaluation Training**: Practice evaluating chess positions and compare with Stockfish's assessment
- **🏆 Scoring System**: 
  - Generous scoring tiers (Perfect: 0-30cp, Excellent: 31-75cp, Great: 76-150cp)
  - Streak bonuses for guesses within 1.5 pawns
  - Combo multipliers and perfect streak bonuses
  - Achievement system with milestones
- **🔊 Sound Effects**: Chess.com audio effects for moves and game events
- **📊 Statistics**: Track your progress, best scores, and achievements
- **🎨 Modern UI**: Dark theme with Material-UI components
- **⚡ Fast Performance**: Optimized architecture with 40% component reduction

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ 
- npm or yarn
- SQLite3

### Installation

1. Clone the repository:
```bash
git clone https://github.com/RNDev666/eval-guesser.git
cd eval-guesser
```

2. Install dependencies:
```bash
npm install
```

3. Set up the database:
```bash
# Generate Prisma client
npx prisma generate

# Run migrations
npx prisma migrate dev

# Import puzzle database (if you have a CSV file)
node scripts/import-puzzles.js puzzles.csv
```

4. Start the development server:
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to play!

## 📝 Available Scripts

- `npm run dev` - Start development server with Turbopack
- `npm run build` - Build for production
- `npm start` - Run production server
- `npm run lint` - Run ESLint
- `npx prisma studio` - Open database GUI

## 🏗️ Architecture

### Tech Stack
- **Framework**: Next.js 15 with App Router
- **Language**: TypeScript
- **UI**: Material-UI (MUI) v7
- **Chess Board**: Chessground (lichess board library)
- **Chess Logic**: chess.js
- **Database**: SQLite with Prisma ORM
- **Chess Engine**: Stockfish.js (WASM)
- **Styling**: CSS-in-JS with emotion
- **Sound**: Custom sound system with Chess.com audio

### Project Structure

```
eval-guesser/
├── app/
│   ├── components/         # React components (consolidated)
│   │   ├── Game.tsx        # Main game controller
│   │   ├── ChessgroundBoard.tsx  # Unified board (game & analysis)
│   │   ├── EvalBar.tsx     # Unified eval bar (3 modes)
│   │   ├── BoardLayout.tsx # Unified layout component
│   │   ├── BoardWrapper.tsx # Pure board state manager
│   │   └── ...
│   ├── play/
│   │   └── classic/        # Classic game mode route
│   ├── analysis/           # Analysis mode route
│   ├── hooks/              # Custom React hooks
│   │   └── useGameReducer.ts    # Game state management
│   ├── lib/                # Utility libraries
│   │   ├── global-sounds.ts     # Sound management system
│   │   └── stockfish-engine.ts  # Chess engine wrapper
│   └── api/                # API routes
├── prisma/
│   └── schema.prisma       # Database schema
├── public/
│   ├── stockfish.js        # Stockfish WASM worker
│   └── stockfish.wasm      # Stockfish WASM binary
└── scripts/
    └── import-puzzles.js   # Puzzle import script
```

### Recent Improvements

- **Component Consolidation**: 40% reduction in components through unification
- **Proper Navigation**: Homepage is pure landing, game at `/play/classic`
- **Reliable Initialization**: Callback ref pattern for Chessground
- **Better UX**: Evaluation always visible, more lenient scoring
- **Performance**: Homepage only 2.36 kB, route-based code splitting

## 🎮 How to Play

### Classic Mode
1. Look at the chess position presented
2. Evaluate who is better (White or Black) and by how much
3. Drag the evaluation bar to input your guess (value always visible)
4. Submit your guess when ready
5. See how close you were to the computer evaluation
6. Puzzle auto-advances after 2 seconds on correct answers
7. Build your streak (within 1.5 pawns counts as correct)!

### Analysis Board
1. Navigate to `/analysis` from the main menu
2. Make moves freely on the board
3. View real-time engine evaluation
4. See the top 3 recommended moves
5. Navigate through move history
6. Use keyboard shortcuts:
   - ← → : Navigate moves
   - ↑ ↓ : Jump to start/end
   - F : Flip board

## 🎵 Sound System

The app features a comprehensive sound system using Chess.com's audio effects:
- Move sounds (regular, capture, castle, check, promotion)
- Game events (start, correct/incorrect evaluation)
- Result feedback based on 150cp threshold
- Volume controls and mute toggle in the header

## 🏆 Scoring System

### Updated Scoring Tiers (More Generous)
- **Perfect**: 0-30 centipawns (was 0-25)
- **Excellent**: 31-75 centipawns (was 26-50)
- **Great**: 76-150 centipawns (was 51-100)
- **Good**: 151-250 centipawns (was 101-200)
- **Okay**: 251-400 centipawns
- **Miss**: 400+ centipawns

### Streak System
- **Streak counts**: Guesses within 150 centipawns (1.5 pawns)
- **Multipliers**: 
  - 3+ streak: 1.2x
  - 5+ streak: 1.5x
  - 10+ streak: 2.0x
  - 20+ streak: 3.0x

### Achievements
- Unlock achievements for milestones
- Track perfect streaks and total puzzles solved
- Score-based achievements

## 🔧 Configuration

### Environment Variables
Create a `.env.local` file:
```
DATABASE_URL="file:./puzzles.db"
```

### CLAUDE.md
The project includes a CLAUDE.md file with specific instructions for AI assistants working with the codebase, documenting the consolidated architecture and patterns.

## 📚 API Routes

- `/api/puzzles/random?includeSolution=true` - Get a random puzzle with solution
- `/api/puzzles/[id]` - Get specific puzzle
- `/api/puzzles/[id]/solution` - Get puzzle solution
- `/api/puzzles/by-theme` - Get puzzles by theme
- `/api/puzzles/by-rating` - Get puzzles by rating range
- `/api/puzzles/stats` - Get puzzle statistics

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- Chess positions from Lichess puzzle database
- Board rendering by Chessground (Lichess)
- Sound effects from Chess.com
- Chess engine powered by Stockfish
- UI components from Material-UI