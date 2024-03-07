
<svelte:head>
	<title>My projects!</title>
</svelte:head>
<script> import projects from '$lib/projects.json'; </script>
<h1><div class="projects">

    {#each projects as p}
    <article>
        <h2>{p.title}</h2>
        <img src={p.image} alt="">
        <p>{p.description}</p>
    </article>
    {/each}
</div>
</h1>