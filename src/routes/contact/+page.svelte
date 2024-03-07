<svelte:head>
	<title>Contact me</title>
</svelte:head>

<form action="mailto:maddiemit123@gmail.com" method="POST" enctype="text/plain">
  <label for="Email"> Email: <input name="email" type="email" /></label>
  <label for="Subject"> Subject: <input name="subject" /> </label>
  <label for="body"> Body: <textarea name="body"></textarea></label>
  <button> submit! </button>
</form>
