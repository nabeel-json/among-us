<script>
  import Hero from "./lib/Hero.svelte";
  import Navbar from "./lib/Navbar.svelte";
  import Phone from "./lib/Phone.svelte";
  import Youtube from "./lib/Youtube.svelte";


</script>

<div id="hero">
  <Navbar />
  <Hero />
  <Youtube />
  <Phone />
</div>

<style>
  :global(body) {
    background-color: #181818;
    color: #f4f4f4
  }

  :global(html) {
    scroll-behavior: smooth;
  }

  #hero {
    background-color: #000000;
    color: whitesmoke;
  }
</style>