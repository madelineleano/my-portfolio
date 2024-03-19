<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";
  import * as d3 from "d3";
  import Pie from "$lib/Pie.svelte";
  export let hLevel = 2;

  let query = "";

  let rolledData = d3.rollups(
    projects,
    (v) => v.length,
    (d) => d.year
  );
  let pieData = rolledData.map(([year, count]) => {
    return { value: count, label: year };
  });

  
  let filteredProjects;

  $: filteredProjects = projects.filter(project => {
	let values = Object.values(project).join("\n").toLowerCase();
	return values.includes(query.toLowerCase());
});



</script>

<svelte:head>
  <title>My projects!</title>
</svelte:head>

<h1>{projects.length} projects</h1>



<Pie data={pieData} />

<input
  type="search"
  bind:value={query}
  aria-label="Search projects"
  placeholder="🔍 Search projects…"
/>

<div class="projects">
  {#each filteredProjects as p }
    <article>
      <Project info={p} />
    </article>
  {/each}
</div>


