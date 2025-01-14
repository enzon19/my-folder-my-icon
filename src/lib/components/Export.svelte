<script>
  function downloadPNG() {
    const preview = document.querySelector('#preview');
  }
</script>

<div class="grid grid-flow-row md:grid-cols-2 gap-2">
  <button onclick={downloadPNG} class="py-2 px-4 bg-[#62cdfe] text-black font-bold rounded-lg">Download ICO</button>
  <button onclick={downloadPNG} class="py-2 px-4 bg-neutral-600 rounded-lg">Download PNG</button>
  <button onclick={downloadPNG} class="py-2 px-4 bg-neutral-600 rounded-lg">Export Icon Settings</button>
  <button onclick={downloadPNG} class="py-2 px-4 bg-neutral-600 rounded-lg">Import Icon Settings</button>
</div>