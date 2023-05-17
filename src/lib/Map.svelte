<script>
  import { onMount, onDestroy } from "svelte";

  let mapElement;
  let map;
  let trucks = [];

  onMount(async () => {
    const leaflet = await import("leaflet");

    leaflet.Icon.Default.imagePath = "/";

    leaflet.Icon.Default.mergeOptions({
      iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
      iconUrl: require("leaflet/dist/images/marker-icon.png"),
      shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
    });

    map = leaflet.map(mapElement).setView([37.7773, -122.4196], 12);

    if (map) {
      fetch("https://data.sfgov.org/resource/rqzj-sfat.json")
        .then((resp) => resp.json())
        .then((data) => {
          trucks = data;
        })
        .finally(() => {
          for (let i = 0; i < trucks.length; i++) {
            leaflet
              .marker([Number(trucks[i].latitude), Number(trucks[i].longitude)])
              .addTo(map)
              .bindPopup(
                `${trucks[i].applicant}<br>${
                  trucks[i].fooditems || "no info given"
                }`
              );
          }
        });
    }

    leaflet
      .tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
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
    height: 600px;
    border: solid 4px lightslategray;
  }
</style>
