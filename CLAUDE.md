# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

World Geography Quiz - An interactive web-based quiz application built with Vue 3 and Vite. The app presents users with 10 random geography questions from a pool of 20+ questions, tracks their score, and provides instant feedback.

## Development Commands

```bash
npm run dev      # Start development server at http://localhost:5173
npm run build    # Create production build in dist/
npm run preview  # Preview production build
```

## Architecture & Key Components

### Component Structure
- **QuizContainer.vue** - Main component that manages quiz state, question flow, and score tracking
- **QuestionCard.vue** - Displays individual questions and handles answer selection
- **ScoreBoard.vue** - Shows current score and progress through the quiz
- **ResultScreen.vue** - Displays final results with score percentage
- **App.vue** - Root component with welcome screen and quiz container mounting

### State Management
- Quiz state is managed in QuizContainer using Vue 3 Composition API
- Components communicate via props and emit events
- No external state management library is used

### Data Flow
1. Questions are imported from `src/data/questions.js` 
2. QuizContainer randomly selects 10 questions when quiz starts
3. User answers are validated immediately with visual feedback
4. Score is tracked and displayed in real-time
5. Results screen shows final score and allows restart

## Adding/Modifying Questions

Questions are stored in `src/data/questions.js`. Format:
```javascript
{
  id: [unique_number],
  question: "Question text?",
  options: ["Option 1", "Option 2", "Option 3", "Option 4"],
  correct: [0-3], // Index of correct answer
  category: "category-name"
}
```

## Important Notes

- The app uses Vite's development server - no backend required
- All quiz logic runs client-side
- Questions are randomized on each quiz start
- The app is fully responsive and works on mobile devices
- No external API calls or database connections