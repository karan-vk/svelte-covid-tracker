<script>
  import { onMount } from "svelte";
  import CountrySelect from "./Components/CountrySelect.svelte";
  import DataBlocks from "./Components/DataBlocks.svelte";
  import DataTile from "./Components/DataTile.svelte";

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
  onMount(async () => {
    const data = await fetchCovidData();
    dataDate = data.Date;
    stats = data.Global;
    countries = data.Countries;
    isLoading = false;
  });
  function changeCountry(e) {
    stats = e.detail;
    title = e.detail.Country;
  }
</script>

<Header />
<div class="container">
  {#if isLoading}
    <!-- content here -->
    <Loading />
  {:else}
    <DataTile {dataDate} {title} />
    <DataBlocks {stats} />
    <CountrySelect {countries} on:get-country={changeCountry} />
  {/if}
</div>

<style>
</style>
