<script lang="ts">
  import Footer from "./lib/Footer.svelte";
  import Map from "./lib/Map.svelte";

  let apiData = [];

  function fetchMapData() {
    fetch(`https://data.sfgov.org/resource/rqzj-sfat.json`)
      .then((resp) => resp.json())
      .then((data) => {
        apiData = data;
      });
  }
</script>

<main>
  <h1>
    foodski,
    <span>a food truck locator </span><span class="truck-emoji">🚚</span>
  </h1>
  <button on:click|once={fetchMapData}>Find Food!</button>
  <Map trucks={apiData} />
  <Footer />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  button {
    margin-bottom: 2.5rem;
  }

  span {
    text-transform: none;
    color: black;
    font-size: 2rem;
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
</style>
