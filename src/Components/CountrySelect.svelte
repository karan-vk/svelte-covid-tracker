<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  export let countries = [];
  let selected = 0;

  function onChangeC() {
    if (selected !== 0) {
      const country = countries.find((item) => item.ID === selected);
      dispatch("get-country", country);
    } else {
      dispatch("get-country", null);
    }
  }
</script>

<select
  bind:value={selected}
  on:change={onChangeC}
  on:blur={onChangeC}
  class="form-select rounded block w-full border p-3 mt-10"
>
  <option value="0">Select country</option>

  {#each countries as country}
    <!-- content here -->
    <option value={country.ID}>
      {country.Country}
    </option>
  {/each}
</select>
