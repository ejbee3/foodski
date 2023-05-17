<script lang="ts">
  import Footer from "./lib/Footer.svelte";
  import Map from "./lib/Map.svelte";
</script>

<main>
  <h1>
    foodski,
    <span>a food truck locator </span><span class="truck-emoji">🚚</span>
  </h1>
  <figure>
    <Map />
    <p>
      CSS design by <a href="https://codepen.io/kirkone/pen/VwEBOYZ">KirK</a>
    </p>
  </figure>
  <Footer />
</main>

<style>
  main {
    text-align: center;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
    margin-top: 0;
    margin-bottom: 0.5rem;
  }

  span {
    text-transform: none;
    color: black;
    font-size: 2rem;
  }

  p {
    font-size: 0.8rem;
    text-align: right;
    margin: 0.2rem 0 0 0;
    font-style: italic;
  }

  .truck-emoji {
    -webkit-transform: scaleX(-1);
    transform: scaleX(-1);
    display: inline-block;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  figure {
    width: auto;
    margin: auto;
    padding: 3rem 3rem 1.5rem 3rem;

    background-color: hsl(0deg 0% 100%);

    border-width: 1rem;
    border-style: solid;
    border-top-color: hsl(0deg 0% 100%);
    border-right-color: hsl(0deg 0% 97%);
    border-bottom-color: hsl(0deg 0% 94%);
    border-left-color: hsl(0deg 0% 97%);

    box-shadow: var(--shadow), var(--shadow-inset);
  }
</style>
