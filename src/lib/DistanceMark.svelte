<script>
  import { fade, slide } from "svelte/transition";
  import { searchTermDistanceMark, selectedAthlete } from "../stores/stores.js";

  export let distanceMark, index;

  function toggleDistanceMark(distanceMark) {
    $searchTermDistanceMark = $searchTermDistanceMark == "" ? distanceMark : "";
  }
</script>

<div transition:slide class="column">
  <div>
    <div on:click={() => toggleDistanceMark(distanceMark[0])} class="table-header underline-on-hover font-bold pointer">
      {distanceMark[0]}
    </div>
    {#each distanceMark[1] as passing}
      <div transition:fade on:click={() => ($selectedAthlete = passing[1].person.uuid)} class:highlight={$selectedAthlete == passing[1].person.uuid} class="table-cell underline-on-hover pointer" id={passing[1].person.uuid}>
        {passing[1].rank ? passing[1].rank + "." : ""}
        {index === 0 ? passing[1].person.name : passing[1].person.firstName.slice(0, 1) + passing[1].person.lastName.slice(0, 1)}
        {passing[1].timeDifference ? passing[1].timeDifference : ""}
      </div>
    {/each}
  </div>
</div>

<style>
  :global(.table-header) {
    background-color: wheat;
    color: black;
    padding: 0.5em 0.5em 0.5em 0.5em;
    margin: 0.5em 0 0.5em 0;
  }

  :global(.table-cell) {
    padding: 0.2em 0 0.2em 0.5em;
    margin: 0 0 0 0;
  }

  :global(.column) {
    display: flex;
    flex-direction: column;
    background-color: #f1f1f1;
    margin: 0.5em 0 0 0.5em;
  }

</style>
