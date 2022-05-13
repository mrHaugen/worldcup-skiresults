<script>
  import { fly } from "svelte/transition";
  import { selectedAthlete } from "../stores/stores.js";

  export let distanceMark;

  const details = [
    { property: "rank", label: "Rank" },
    { property: "timeDifference", label: "Time difference" },
    { property: "duration", label: "Duration" },
    { property: "country", label: "Country" },
  ];
</script>

{#each details as detail}
  <div transition:fly={{ x: -200, duration: 500 }} class="column">
    <div>
      <div transition:fly={{ x: -200, duration: 500 }} class="table-header font-bold">{detail.label}</div>
      {#each distanceMark[1] as passing}
        <div transition:fly={{ x: -200, duration: 500 }} class:highlight={$selectedAthlete == passing[1].person.uuid} class="table-cell">
          {passing[1][detail.property] ? passing[1][detail.property] : passing[1].person[detail.property] ? passing[1].person[detail.property] : "-"}
        </div>
      {/each}
    </div>
  </div>
{/each}
