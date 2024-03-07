<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";
  export let hLevel = 2;
</script>

<svelte:head>
  <title>My projects!</title>
</svelte:head>

<h1>
  <div class="projects">
    <h1>{projects.length} projects</h1>

    {#each projects as p}
      <article>
        <Project info={p} />
      </article>
    {/each}
  </div>
</h1>
