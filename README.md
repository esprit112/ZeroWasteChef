# Zero Waste Chef

A recipe app that starts with what is already in the kitchen.

Most recipe apps begin with a shopping list. That is backwards if the point is to waste less: the food is already in the fridge, going soft, and what you need is a reason to use it tonight.

## How it works

1. Describe what you have, or photograph the open fridge or the pantry shelf.
   The placeholder sets the tone: "2 wilted carrots, half an onion, some stale bread..."
2. Gemini reads the list or the image and returns recipes: a title, difficulty, cook time and instructions.
3. Share a recipe, or save it as a PDF to keep.

The photo path is for the honest case. Nobody wants to type out the contents of a vegetable drawer at 6pm.

## Status

Early build. The recipes are not saved between sessions, and there is no test suite yet.

## Running it

```bash
npm install
echo "GEMINI_API_KEY=your-key" > .env.local
npm run dev
```

## How it is built

- **React and TypeScript**, on Vite.
- **Gemini** via `@google/genai`. Text and an optional image go into the same request; the image is sent as inline base64.
- **jsPDF** produces the saved recipe, because a recipe you cannot get out of the app is a recipe you will not cook.
- **Web Share API** where the browser has it, clipboard as the fallback.

```
src/App.tsx   interface, request handling, PDF and share
```

## Limits worth knowing

- **Ingredients and quantities are the model's guess.** Check what it tells you to put in before you put it in.
- **Allergens are not checked.** It will happily suggest a peanut sauce for a nut allergy. Read the recipe as a suggestion from a confident stranger, not as a dietitian.
- **The API key is compiled into the client bundle** through Vite's `define`. Anyone who can load the page can extract it. Run it locally with your own key; do not deploy it publicly without moving the call behind a server.
- **No persistence.** Refresh and the recipes are gone.

## Licence

No licence file. The code is public to read; all rights are reserved, and it is not intended for reuse or deployment as it stands.

---

Built by [Martin Greer](https://github.com/esprit112).
