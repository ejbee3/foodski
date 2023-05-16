<script lang="ts">
</script>

<main>
  <h1>
    foodski,
    <span>a food truck locator </span><span class="truck-emoji">🚚</span>
  </h1>
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
