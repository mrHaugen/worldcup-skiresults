<script>
  import data from "../assets/data.json";
  import RaceInfo from "./RaceInfo.svelte";
  import DistanceMark from "./DistanceMark.svelte";
  import DistanceDetails from "./DistanceDetails.svelte";
  import CountryFilter from "./CountryFilter.svelte";

  import { searchTermCountry, searchTermDistanceMark } from "../stores/stores.js";

  $: filteredResults = Object.entries(data.locations)
    //filter athletes by nationality
    .map((element) => {
      if ($searchTermCountry) {
        return { ...element, 1: Object.entries(element[1]).filter((subElement) => subElement[1].person.country === $searchTermCountry) };
      } else {
        // if no country is given, show all countries
        return { ...element, 1: Object.entries(element[1]) };
      }
    })
    //filter athletes by distance mark
    .filter((item) => item[0].indexOf($searchTermDistanceMark) !== -1);
</script>

<div class="container">
  <!-- block with info about the race -->
  <RaceInfo {data} />

  <!-- toggle hide/show norwegian atheletes -->
  <CountryFilter />

  <div class="result-table">
    {#each filteredResults as distanceMark, index}
      {#if distanceMark[0] === $searchTermDistanceMark || $searchTermDistanceMark === ""}
        <DistanceMark {distanceMark} {index} />
      {/if}

      <!-- show athlete details for the selected distance -->
      {#if distanceMark[0] === $searchTermDistanceMark}
        <DistanceDetails {distanceMark} />
      {/if}
    {/each}
  </div>
</div>

<style>

  :global(.underline-on-hover:hover) {
    text-decoration: underline;
  }

  :global(.underline) {
    text-decoration: underline;
  }

  :global(.pointer) {
    cursor: pointer;
  }

  :global(.highlight) {
    color: white;
    background-color: tan;
  }

  .container {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    width: 100%;
    text-align: left;
    background-color: white;
  }
  .result-table {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    width: 100%;
    text-align: left;
    background-color: white;
  }

  :global(.font-bold) {
    font-weight: 700;
  }
</style>
