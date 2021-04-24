<script>
  import Icon from "fa-svelte";
  import { faViruses } from "@fortawesome/free-solid-svg-icons/faViruses";
  const icon = faViruses;
</script>

<header class="text-center bg-blue-800 text-white p-4 mb-10">
  <div class="text-3xl md:text-5xl font-bold mb-3">
    <Icon {icon} /> Covid-19 tracker
  </div>
  <p>
    by K <a href="https://github.com/karan-vk" rel="noreferrer" target="_blank">
      github</a
    >
  </p>
</header>
