# Kababus Game

Kababus Game is a lightweight web-based Hebrew logic puzzle generator.  
The user enters a topic and selects a difficulty level, and the system generates a short “תרתי משמע” (double-meaning) logic clue based on that topic.

The game is designed as a simple, single-page web app that calls a secure backend API, which in turn generates the puzzle using an LLM.

---

## Features

- Free-text topic input
- Three difficulty levels: easy, medium, hard
- Automatically generated Hebrew logic clues
- Hints system (three progressive hints)
- Answer reveal option
- Fully client-side interface with secure backend API

---

## Project Structure

The project consists of two main parts:

1. Frontend (static HTML file)
2. Backend API (Cloudflare Worker)

### Frontend
- File: `kababus-game.html`
- Pure HTML, CSS, and JavaScript
- Sends a POST request to the backend API
- Displays the generated puzzle and handles user interaction

### Backend
- Cloudflare Worker
- Receives topic and difficulty
- Calls the LLM API
- Returns a structured JSON puzzle

---

## API Contract

### Request (POST)

POST /generate
Content-Type: application/json

{
"topic": "חיות",
"difficulty": "medium"
}


### Response

{
"clue": "משפט החידה (3)",
"answer": "מילה",
"hints": [
"רמז כללי",
"רמז מבני",
"רמז חזק"
],
"explanation": "הסבר קצר"
}


---

## How to Run Locally

1. Open `kababus-game.html` in a browser.
2. Ensure the backend API URL in the file points to a deployed Worker.
3. Enter a topic and difficulty to generate a puzzle.

---

## Deployment

### Frontend (GitHub Pages)

1. Create a new GitHub repository.
2. Upload `kababus-game.html`.
3. Rename it to `index.html`.
4. Go to:
   Settings → Pages
5. Set:
   - Source: Deploy from a branch
   - Branch: main
   - Folder: / (root)
6. Save and wait for deployment.
7. GitHub will provide a public URL.

### Backend (Cloudflare Worker)

1. Create a new Worker.
2. Add an environment variable:
   - Name: `OPENAI_API_KEY`
   - Value: your API key
3. Paste the Worker code.
4. Deploy the Worker.
5. Copy the Worker URL.
6. Update the frontend to call that URL.

---

## Puzzle Generation Logic

The backend sends a structured prompt to the language model with:

- Strict rules about valid Hebrew words
- Topic-based constraints
- Difficulty-specific behavior
- Allowed cryptic techniques
- Required JSON output format

The model returns:

- A single clue
- The correct answer
- Three hints
- A short explanation

---

## Security Notes

- The API key is stored only in the backend.
- The frontend never exposes the API key.
- All LLM calls are made through the Worker.

---

## Requirements

- Modern web browser
- GitHub account (for hosting)
- Cloudflare account (for backend)
- OpenAI API key with credit

---

## License

Internal or personal use unless otherwise specified.
