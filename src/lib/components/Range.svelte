<script>
  let { label, id, min, max, value = $bindable() } = $props();
</script>

<div class="flex flex-row items-center gap-2 p-2 bg-neutral-800/50 rounded-lg border shadow border-neutral-800">
  <label class="min-w-max" for={id}>{label}</label>
  <input type="range" {id} {min} {max} class="w-full" bind:value/>
  <input type="number" {min} {max} class="bg-neutral-700 rounded-lg text-white px-2 py-0.5 outline-none w-20" bind:value>
</div>