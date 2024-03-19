<slot />
<script>

  let localStorage = globalThis.localStorage ?? {};

  let colorScheme = localStorage.colorScheme ? localStorage.colorScheme : "light dark";

  localStorage.colorScheme = colorScheme;


  let root = globalThis?.document?.documentElement;

  root?.style.setProperty("color-scheme", colorScheme);
  $: root?.style.setProperty("color-scheme", colorScheme);






</script>



<label class="color-scheme">
  Theme:
  <select bind:value={ colorScheme }>
    <option value="light"> Light </option>

    <option value="light dark"> Automatic </option>

    <option value="dark"> Dark </option>
  </select>
</label>

<style>
  .color-scheme {
    position: absolute;
    top: 1rem;
    right: 1rem;
    font-size: 80%;
  }
</style>
