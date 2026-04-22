<script lang="ts">
  import type { Snippet } from "svelte";

  let { children }: { children: Snippet } = $props();
</script>

<header>
  <h2><a href="/">My Notes</a></h2>
  <h2><a href="/svelte">Made with SvelteKit</a></h2>
</header>

{@render children()}

<style>
  header {
    padding: 1rem 2rem;
    background: #ff3e00;
    margin-bottom: 2rem;
  }

  header h2 {
    margin: 0;
  }

  header a {
    color: white;
    text-decoration: none;
  }
</style>
