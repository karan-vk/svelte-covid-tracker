<script>
  // import { onMount } from "svelte";
  import CountrySelect from "./Components/CountrySelect.svelte";
  import DataBlocks from "./Components/DataBlocks.svelte";
  import DataTile from "./Components/DataTile.svelte";
  import { fade } from "svelte/transition";
  import { cubicIn } from "svelte/easing";

  import Header from "./Components/Header.svelte";
  import Loading from "./Components/Loading.svelte";
  let dataDate = null;
  let stats = null;
  let countries = null;
  let title = "Global";
  let isLoading = true;
  const fetchCovidData = async () => {
    const res = await fetch("https://api.covid19api.com/summary");
    const data = await res.json();
    return data;
  };
  const reset = async () => {
    isLoading = true;
    const data = await fetchCovidData();
    dataDate = data.Date;
    stats = data.Global;
    title = "Global";
    countries = data.Countries;
    isLoading = false;
  };
  function changeCountry(e) {
    stats = e.detail;
    title = e.detail.Country;
  }
  reset();
</script>

<Header />
<div class="container">
  {#if isLoading}
    <Loading />
  {:else}
    <div transition:fade={{ easing: cubicIn }}>
      <DataTile {dataDate} {title} />
      <DataBlocks {stats} />
      <CountrySelect {countries} on:get-country={changeCountry} />
      {#if stats.Country}
        <button
          on:click={reset}
          v-if="stats.Country"
          class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-500"
        >
          Clear country
        </button>
      {/if}
    </div>
  {/if}
</div>

<style>
</style>
