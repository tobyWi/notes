# 05 - Do It Yourself

<img src="https://media.giphy.com/media/hRyKLMNS6MiZ5oEwBL/giphy.gif" width="400"/>

Exercise time! 🎉

In this lesson, you'll build a notes app using Svelte 5 and SvelteKit.

### Setup
```
npm install
npm run dev
```

### What to implement
You've been given the project scaffold, a `Note` type, and empty component stubs. Implement the following:

1. **`src/routes/+page.svelte`** — the main page
   - A `$state` array of notes
   - Two text inputs (title and body) bound to local state
   - An "Add Note" button that pushes a new note into the array
   - Render each note using the `NoteItem` component

2. **`src/lib/components/NoteItem.svelte`** — a single note card
   - Displays the note's title and body
   - Has a "Delete" button that calls a callback prop to remove the note

You've successfully completed this lesson when:

1. `npm run dev` starts without errors
2. Filling in both inputs and clicking "Add Note" shows a new note card below
3. Clicking "Delete" on a note removes it from the list
4. Your notes survive client-side navigation (click away and back — they should still be there)

### Extra Challenge
Persist notes to `localStorage` so they survive a full page refresh. Hint: use `$effect` to watch the notes array and write to `localStorage`, and `$state` initialised from `localStorage` on load.

A reference solution is in the `Solution/` folder if you get stuck.
