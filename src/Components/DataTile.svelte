<script>
  import dayjs from "dayjs";

  export let title = null;
  export let dataDate = null;
  $: timestamp = dayjs(dataDate).format("MMMM D YYYY , h:mm:ss a");
</script>

<div class="text-center">
  <h2 class="text-3xl font-bold">{title}</h2>
  <div class="text-2xl mt-4 mb-10">{timestamp}</div>
</div>
