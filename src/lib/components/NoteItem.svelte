<script lang="ts">
  import type { Note } from "$lib/types";

  // TODO: Declare props using $props()
  // This component needs: note (type Note) and ondelete (a callback function)
  let { note, ondelete }: { note: Note; ondelete: (id: string) => void } =
    $props();
</script>

<!-- TODO: Render the note's title and body -->
<!-- TODO: Add a Delete button that calls ondelete with the note's id -->
<div class="note-card">
  <h2>{note.title}</h2>
  <p>{note.body}</p>
  <button onclick={() => ondelete(note.id)}>Delete</button>
</div>

<style>
  /* Optional: style your note card */
</style>
