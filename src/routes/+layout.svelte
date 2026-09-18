<script lang="ts">
  import '../app.css';
  let { children } = $props();
</script>

<svelte:head>
  <title>Ryan Juska | Engineer & Developer Portfolio</title>
</svelte:head>

{@render children()}
