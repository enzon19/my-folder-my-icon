<script>
  let { label, id, value = $bindable() } = $props();
</script>

<div class="flex flex-row items-center gap-2 p-2 bg-neutral-800/50 rounded-lg border shadow border-neutral-800">
  <input type="color" class="picker rounded-full outline-none w-6 h-6 border-2 cursor-pointer" {id} bind:value/>
  <label for={id}>{label}</label>
</div>

<style>
  .picker::-webkit-color-swatch-wrapper {
    padding: 0; 
  }
  .picker::-webkit-color-swatch {
    border: none;
    border-radius: 50%;
  }
</style>