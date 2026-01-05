# MathsKit

Single-file React math practice app for kids. All code in `index.html`.

## Stack
- React 18 (CDN, Babel transpiled)
- Tailwind CSS (CDN)
- No build step - runs directly in browser

## Architecture

```
index.html
├── DIFFICULTY_CONFIG     # easy/medium/hard settings (ranges, timers)
├── OPERATIONS            # +, −, ×, ÷
├── generateQuestion()    # Creates {a, b, answer, symbol, missingPosition, correctAnswer}
├── generateQuestions()   # Deduped batch generation
└── Components:
    ├── App               # State: screen, settings, questions, results, isRetrySession
    ├── SetupScreen       # Operation/difficulty/timer selection
    ├── PracticeScreen    # Questions, timer, number pad, feedback
    └── ResultsScreen     # Score, mistakes review, practice-again button
```

## Key Features
- **Missing Numbers**: `? + 5 = 8` format. Frequency varies by difficulty (Easy: 0%, Medium: 25%, Hard: 35%)
- **Practice Mistakes**: Retry wrong answers. Uses `isRetrySession` flag to skip celebration
- **Timed Mode**: Per-question countdown with circular timer

## Settings State
```js
{ operations, mixedMode, difficulty, timed, timerDuration,
  questionCount, allowNegatives, missingNumbers }
```

## Question Object
```js
{ a, b, answer, symbol, operation, missingPosition, correctAnswer }
// missingPosition: 'a' | 'b' | 'result'
// correctAnswer: the value user must enter (differs based on missingPosition)
```

## Conventions
- Handlers: `handleX` in App, passed as `onX` props
- Colors: teal (primary), coral (secondary), amber (practice mistakes)
- Dark mode: Tailwind `dark:` classes, toggled via `darkMode` state
