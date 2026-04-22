<script lang="ts">
  import NoteItem from "$lib/components/NoteItem.svelte";
  import type { Note } from "$lib/types";

  // TODO: Create $state variables for the title and body inputs
  let title: string = $state("");
  let body: string = $state("");
  let notes: Note[] = $state([]);

  function addNote() {
    notes = [...notes, { id: crypto.randomUUID(), title, body }];
    title = "";
    body = "";
  }

  function deleteNote(id: string) {
    notes = notes.filter((n) => n.id !== id);
  }

  // Runs once on mount — loads from localStorage
  $effect(() => {
    notes = JSON.parse(localStorage.getItem("notes") || "[]");
  });

  // Runs whenever notes changes — saves to localStorage
  $effect(() => {
    localStorage.setItem("notes", JSON.stringify(notes));
  });
</script>

<main>
  <section class="form">
    <input type="text" placeholder="Title" bind:value={title} />
    <textarea placeholder="Body" bind:value={body}></textarea>
    <button
      type="submit"
      onclick={addNote}
      disabled={!title.trim() || !body.trim()}>Add Note</button
    >
  </section>

  <section class="notes">
    {#each notes as note (note.id)}
      <NoteItem {note} ondelete={deleteNote} />
    {/each}
  </section>
</main>

<style>
  main {
    max-width: 600px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  .form {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-bottom: 2rem;
  }

  input,
  textarea {
    padding: 0.5rem;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  textarea {
    min-height: 80px;
    resize: vertical;
  }

  button {
    padding: 0.5rem 1rem;
    background: #ff3e00;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
    &:disabled {
      background: #ccc;
      cursor: not-allowed;
    }
  }

  .notes {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>
