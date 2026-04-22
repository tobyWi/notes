<script lang="ts">
  import type { Note } from '$lib/types';

  let { note, ondelete }: { note: Note; ondelete: (id: string) => void } = $props();
</script>

<article>
  <h3>{note.title}</h3>
  {#if note.body}
    <p>{note.body}</p>
  {/if}
  <button onclick={() => ondelete(note.id)}>Delete</button>
</article>

<style>
  article {
    border: 1px solid #e0e0e0;
    border-radius: 6px;
    padding: 1rem;
    background: #fafafa;
  }

  h3 {
    margin: 0 0 0.5rem;
  }

  p {
    margin: 0 0 0.75rem;
    color: #555;
  }

  button {
    padding: 0.25rem 0.75rem;
    background: transparent;
    color: #cc0000;
    border: 1px solid #cc0000;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.875rem;
  }

  button:hover {
    background: #cc0000;
    color: white;
  }
</style>
