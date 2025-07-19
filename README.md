# World Geography Quiz

A simple, interactive geography quiz web application built with Vue 3 and Vite. Test your knowledge of world capitals, countries, continents, and geographic landmarks!

## Features

- 🌍 **20+ Geography Questions** - Covering capitals, continents, landmarks, and more
- 🎯 **Multiple Choice Format** - Four options per question for easy interaction
- 📊 **Real-time Score Tracking** - See your score and progress as you play
- 🔄 **Randomized Questions** - Each quiz session randomly selects 10 questions
- 💯 **Instant Feedback** - Know immediately if your answer is correct
- 📱 **Responsive Design** - Works seamlessly on desktop and mobile devices
- 🎨 **Clean, Modern UI** - Simple and intuitive interface

## Demo

To see the quiz in action, run the development server (see instructions below).

## Tech Stack

- **Vue 3** - Progressive JavaScript framework
- **Vite** - Fast build tool and development server
- **CSS3** - Modern styling with animations and transitions

## Project Structure

```
world-quiz/
├── src/
│   ├── components/
│   │   ├── QuizContainer.vue    # Main quiz logic and state management
│   │   ├── QuestionCard.vue     # Individual question display
│   │   ├── ScoreBoard.vue       # Score and progress tracking
│   │   └── ResultScreen.vue     # Final quiz results
│   ├── data/
│   │   └── questions.js         # Question database
│   ├── App.vue                  # Root component
│   ├── main.js                  # Application entry point
│   └── style.css                # Global styles
├── index.html
├── package.json
└── vite.config.js
```

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Installation

1. Clone the repository:
```bash
git clone [repository-url]
cd world-quiz
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173`

### Building for Production

To create a production build:

```bash
npm run build
```

The built files will be in the `dist/` directory.

To preview the production build:

```bash
npm run preview
```

## How to Play

1. Click "Start Quiz" on the welcome screen
2. Read each question carefully
3. Select one of the four answer options
4. Get instant feedback on your answer
5. Continue through all 10 questions
6. View your final score and percentage
7. Click "Play Again" to start a new quiz with different questions

## Adding New Questions

To add new questions, edit the `src/data/questions.js` file. Each question should follow this format:

```javascript
{
  id: 21,  // Unique ID
  question: "Your question here?",
  options: ["Option 1", "Option 2", "Option 3", "Option 4"],
  correct: 2,  // Index of correct answer (0-based)
  category: "category-name"
}
```

## Contributing

Feel free to submit issues and enhancement requests!

## License

This project is open source and available under the MIT License.