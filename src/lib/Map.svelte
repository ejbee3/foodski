<script>
  import { onMount, onDestroy } from "svelte";

  let mapElement;
  let map;
  let trucks = [];

  onMount(async () => {
    const leaflet = await import("leaflet");
    const tacoIcon = leaflet.icon({
      iconUrl: "./taco.png",
      iconSize: [52, 48],
      iconAnchor: [35, 55],
      popupAnchor: [-3, -45],
    });

    map = leaflet.map(mapElement).setView([37.7773, -122.4196], 11);

    if (map) {
      fetch("https://data.sfgov.org/resource/rqzj-sfat.json")
        .then((resp) => resp.json())
        .then((data) => {
          trucks = data;
        })
        .finally(() => {
          for (let i = 0; i < trucks.length; i++) {
            leaflet
              .marker(
                [Number(trucks[i].latitude), Number(trucks[i].longitude)],
                { icon: tacoIcon }
              )
              .addTo(map)
              .bindPopup(
                `<b>${trucks[i].applicant}</b><br>${
                  trucks[i].fooditems || "no info given"
                }`
              );
          }
        });
    }

    leaflet
      .tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright" target="_blank" rel="noopener">OpenStreetMap</a> contributors',
      })
      .addTo(map);
  });

  onDestroy(async () => {
    if (map) {
      console.log("Unloading Leaflet map.");
      map.remove();
    }
  });
</script>

<main>
  <div bind:this={mapElement} />
</main>

<style>
  @import "leaflet/dist/leaflet.css";
  main div {
    height: 550px;
    display: block;
    box-shadow: var(--shadow-inset);
    border-width: 3px;
    border-style: solid;
    border-color: hsl(0deg 0% 90%) hsl(0deg 0% 94%) hsl(0deg 0% 97%)
      hsl(0deg 0% 95%);
  }
</style>
