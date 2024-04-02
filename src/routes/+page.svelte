<script>
  import projects from "$lib/projects.json";
  import Project from "$lib/Project.svelte";
</script>

<svelte:head>
  <title>My website!</title>
</svelte:head>

<h1>Madeline Leano</h1>
<img src="images/parisphoto.jpeg" alt="photo of me in paris" />
<p>
  Hi I am Madeline Leano! I am a sophomore studying CS at MIT. I am from Miami
  but currently reside in Boston. Enjoy the website!
</p>

{#await fetch("https://api.github.com/users/madelineleano")}
  <p>Loading...</p>
{:then response}
  {#await response.json()}
    <p>Decoding...</p>
  {:then data}
    <h2>GITHUB STATS</h2>
    <p>Followers: {data.followers}</p>
    <p>Following: {data.following}</p>
    <p>Public Repos: {data.public_repos}</p>
  {:catch error}
    <p class="error">
      Something went wrong: {error.message}
    </p>
  {/await}
{:catch error}
  <p class="error">
    Something went wrong: {error.message}
  </p>
{/await}

<div class="projects">
  <h2>Latest Projects!</h2>
  <br />
  <br />

  {#each projects.slice(0, 3) as p}
    <article>
      <Project info={p} hLevel="3" />
    </article>
  {/each}
</div>
