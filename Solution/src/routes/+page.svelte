<script lang="ts">
  import NoteItem from "$lib/components/NoteItem.svelte";
  import type { Note } from "$lib/types";
  import { browser } from "$app/environment";
  const stored = browser ? localStorage.getItem("notes") : null;

  let notes: Note[] = $state(JSON.parse(stored || "[]"));

  let title = $state("");
  let body = $state("");

  function addNote() {
    if (!title.trim()) return;
    notes = [
      ...notes,
      {
        id: crypto.randomUUID(),
        title: title.trim(),
        body: body.trim(),
      },
    ];
    title = "";
    body = "";
  }

  function deleteNote(id: string) {
    notes = notes.filter((n) => n.id !== id);
  }

  $effect(() => {
    localStorage.setItem("notes", JSON.stringify(notes));
    console.log(browser);
  });
</script>

<main>
  <section class="form">
    <input type="text" placeholder="Title" bind:value={title} />
    <textarea placeholder="Body" bind:value={body}></textarea>
    <button onclick={addNote}>Add Note</button>
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
  }

  .notes {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>
