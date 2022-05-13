<script>
  import { searchTermCountry } from "../stores/stores.js";
</script>

<button
  class="button-country-filter"
  on:click={() => {
    $searchTermCountry ? ($searchTermCountry = "") : ($searchTermCountry = "Norway");
  }}
>
  <span class="font-bold underline">
    {$searchTermCountry ? "Viser norske" : "Viser alle nasjonaliteter"}
  </span>
  ⇆
  {$searchTermCountry ? "vis alle nasjonaliteter" : "vis kun norske"}
</button>

<style>
  .button-country-filter {
    background-color: orange;
    max-width: 330px;
    border-radius: 8px;
    border-style: none;
    color: #ffffff;
    cursor: pointer;
    height: 40px;
    line-height: 20px;
  }

  .button-country-filter:hover {
    background-color: darkorange;
  }
</style>
