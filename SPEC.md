# MathsKit - Arithmetic Practice App

## Overview
A clean, distraction-free arithmetic practice app for children ages 7-9. Single HTML file using React + Tailwind via CDN, hostable on GitHub Pages with no build step.

## Target Audience
- Primary: Children ages 7 and 9
- Goal: Practice addition, subtraction, multiplication (times tables), and division

---

## Technical Stack
- **Framework**: React via CDN
- **Styling**: Tailwind CSS via CDN
- **Font**: Rounded friendly sans-serif (Nunito or Quicksand via Google Fonts)
- **Hosting**: GitHub Pages compatible (single HTML file, no build)
- **Offline**: Online-only (no service worker/PWA)

---

## Screens

### 1. Setup Screen
The entry point where children configure their practice session. Designed for speed - should take ~5 seconds to start practicing.

#### Operation Selection
- Display as large tappable cards with **icon + text label**
- Operations: ➕ Addition, ➖ Subtraction, ✖️ Multiplication, ➗ Division
- Multi-select allowed (can practice multiple operations)
- Additional option: **"Mixed Challenge"** - randomly mixes all four operations with equal weighting

#### Difficulty Selection
- Three large buttons in a row: **Easy | Medium | Hard**
- Visual distinction (size, color) for selected state

#### Difficulty Definitions

| Difficulty | Add/Subtract Range | Times Tables | Timer (per question) |
|------------|-------------------|--------------|---------------------|
| Easy       | 1-10              | 1-5          | 30 seconds          |
| Medium     | 1-20              | 1-10         | 10 seconds          |
| Hard       | 1-50              | 1-12         | 5 seconds           |

#### Timer Toggle
- Simple on/off toggle: **"Timed"** checkbox or switch
- When ON: Uses difficulty-tied per-question countdown
- When OFF: No timer displayed during practice at all

#### Question Count
- Four tappable buttons: **10 | 15 | 20 | 25**

#### Advanced Toggle (Expandable)
- **Negative numbers toggle**: Off by default
  - When ON, subtraction can result in negative answers (e.g., 3 - 8 = -5)
  - When OFF, larger number always comes first

#### Start Button
- Large, prominent **"Start Practice"** button
- Playful bounce animation on tap

#### Dark Mode Toggle
- Small sun/moon icon in top corner
- Always visible on all screens
- Toggles between light and dark themes

---

### 2. Practice Screen
Clean, focused interface for answering questions.

#### Question Display
- Large, centered question in **horizontal format**: `5 + 3 = ?`
- Rounded friendly font, large size for readability

#### Progress Indicator
- **Both** progress bar AND numbers displayed
- Format: Visual bar + "Question 3 of 10"
- Positioned at top of screen, unobtrusive

#### Timer Display (when enabled)
- **Circular countdown** animation
- Circle depletes as time runs out
- Visually clear and engaging
- Hidden completely when timer is disabled

#### Answer Input
- Large input field showing entered digits
- **Subtle orange warning** if answer seems unreasonable (too many digits for the possible answer range)

#### Number Pad
- Large touch-friendly buttons (0-9)
- **Clear button (C)**: Clears entire input
- **Backspace button (⌫)**: Deletes last digit
- **"GO" button**: Submits answer (prominent, different color)
- Grid layout optimized for touch

#### Keyboard Support
- Number keys (0-9) for input
- Backspace/Delete for corrections
- Enter key to submit
- Works alongside on-screen number pad

#### Feedback
- **Correct answer**: Green flash with ✓ checkmark icon, 0.8 second duration
- **Wrong answer**: Red flash with ✗ icon, shows correct answer, 2 second duration
- After feedback, show **"Next" or "Continue" button** to advance (not auto-advance)

#### Exit Option
- Small X or "Quit" button in corner
- Tapping immediately shows Results screen with progress so far
- No confirmation dialog needed

---

### 3. Results Screen
Summary of the practice session.

#### Score Display
- Large, prominent score: **"17/20 (85%)"**
- Fraction format with percentage

#### Time Taken
- Total elapsed time for the session (even if untimed mode)
- Format: "Time: 2m 34s"

#### Mistakes Review
- **Expandable format**: Collapsed summary by default
- Header shows: "3 mistakes - tap to review"
- When expanded, shows each wrong question:
  - The question asked
  - Child's answer
  - Correct answer
- Collapsible back to summary

#### Action Buttons
- **Two equal-sized buttons**:
  - "Play Again" - Same settings, new questions
  - "New Practice" - Return to Setup screen

#### Completion Message
- Simple "Well done!" or "Great practice!" message
- Minimal celebration, calm and focused

---

## Design System

### Color Palette
**Warm & playful** (Duolingo-inspired)

#### Light Mode
- Background: Warm off-white (#FFF9F5 or similar)
- Primary accent: Soft teal/green (#4ECDC4)
- Secondary accent: Warm coral/orange (#FF6B6B)
- Text: Dark gray (#2D3436)
- Success: Green (#27AE60)
- Error: Soft red (#E74C3C)
- Cards: White with subtle shadow

#### Dark Mode
- Background: Dark blue-gray (#1A1A2E)
- Primary accent: Brighter teal (#5DFDCB)
- Secondary accent: Soft coral (#FF8A80)
- Text: Off-white (#F5F5F5)
- Cards: Slightly lighter than background

### Typography
- **Primary font**: Nunito or Quicksand (Google Fonts)
- Question display: Extra large, bold
- Number pad: Large, clear
- UI elements: Medium weight, readable

### Animations
- **Playful bounces**: Spring animations on button presses
- Gentle transitions between screens (fade/slide)
- Bounce effect on correct answers
- Subtle shake on wrong answers

### Touch Targets
- Minimum 48x48px for all interactive elements
- Number pad buttons: Large squares, easy to tap
- Generous spacing between elements

---

## Question Generation Rules

### Addition
- Both operands within difficulty range
- Result can exceed range (e.g., Easy: 8 + 7 = 15 is valid)

### Subtraction
- Default: Larger number always first (result always positive)
- With negative toggle ON: Either order allowed
- Numbers within difficulty range

### Multiplication (Times Tables)
- First operand: 1 to difficulty max (Easy: 1-5, Medium: 1-10, Hard: 1-12)
- Second operand: Same range
- Randomly swap operand order for variety

### Division
- **Clean divisions only** - no remainders
- Generate by: Pick two numbers, multiply them, use product as dividend
- Example: Pick 4 and 7, generate "28 ÷ 4 = ?" or "28 ÷ 7 = ?"
- Divisor and quotient within times table range for difficulty

### Mixed Challenge Mode
- Equal random selection across enabled operations
- No adaptive weighting based on performance

---

## Accessibility

### Color Blind Support
- All feedback uses **colors + icons**
- Correct: Green background + ✓ checkmark
- Wrong: Red background + ✗ icon
- Never rely on color alone

### Touch Accessibility
- Large tap targets throughout
- Clear visual feedback on all interactions
- High contrast in both light and dark modes

---

## Edge Cases

### Input Validation
- Prevent entering more digits than reasonable for answer
- Subtle orange warning when input seems wrong
- Allow negative sign input when negative numbers enabled

### Timer Expiry
- When per-question timer runs out: Mark as wrong, show correct answer, display Next button

### Empty Submit
- "GO" button disabled until at least one digit entered
- Or show gentle prompt if tapped with empty input

### Session Quit
- Quitting mid-session shows results for completed questions
- Incomplete question not counted

---

## State Management

### No Persistence
- Completely stateless between sessions
- No localStorage usage
- Fresh start every time app is loaded

### Session State (in-memory only)
- Current question index
- Answers given (for results review)
- Time tracking (start time, per-question times)
- Current settings (operation, difficulty, question count, timer)

---

## Mobile-First Responsive Design

### Phone Portrait (Primary)
- Full-width number pad
- Stacked layout
- Large touch targets

### Tablet
- Larger question display
- Number pad sized appropriately (not stretched)
- More whitespace

### Desktop
- Centered content with max-width
- Number pad still visible (for mouse clicks)
- Keyboard input fully functional

---

## Non-Goals (Explicitly Excluded)
- User profiles or accounts
- Progress tracking between sessions
- Leaderboards or competitive features
- Sound effects
- Gamification (streaks, badges, points)
- Adaptive difficulty
- Offline support / PWA
- Backend / API integration
