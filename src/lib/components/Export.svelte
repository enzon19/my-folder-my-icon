<script>
	import { icon } from '$lib/icon.svelte.js';
  import { PngIcoConverter } from "$lib/png2icojs.min.js";

  function downloadPNG() {
    const preview = document.querySelector('#preview');
    const image = preview.toDataURL('image/png');

    const link = document.createElement('a');
    link.href = image;
    link.download = `folder-icon-${Date.now().toString()}.png`;
    link.click();
    link.remove();
  }

  async function downloadICO() {
    const preview = document.querySelector('#preview');
    const originalWidth = preview.width;
    const originalHeight = preview.height;

    const resizedCanvas = document.createElement('canvas');
    const ctx = resizedCanvas.getContext('2d');
    resizedCanvas.width = 256;
    resizedCanvas.height = 256;

    ctx.drawImage(preview, 0, 0, originalWidth, originalHeight, 0, 0, 256, 256);

    const imageData = resizedCanvas.toDataURL('image/png');
    const response = await fetch(imageData);
    const pngBlob = await response.blob();

    const converter = new PngIcoConverter();
    const icoBlob = await converter.convertToBlobAsync([{ png: pngBlob }]);

    const link = document.createElement('a');
    link.href = URL.createObjectURL(icoBlob);
    link.download = `folder-icon-${Date.now().toString()}.ico`;
    link.click();
    URL.revokeObjectURL(link.href);
    link.remove();
  }

  let settings = $state(JSON.stringify(icon, null, 2));
  function importSettings(event) {
    try {
      const data = JSON.parse(this.value);
      icon.colors = data.colors;
      icon.image = data.image;
    } catch (e) {
      alert(e);
    }
  }
</script>

<div class="grid grid-flow-row md:grid-cols-2 gap-2">
  <button onclick={downloadICO} class="py-2 px-4 bg-[#62cdfe] text-black font-bold rounded-lg">Download ICO</button>
  <button onclick={downloadPNG} class="py-2 px-4 bg-neutral-600 rounded-lg">Download PNG</button>
</div>
<div class="mt-2 flex flex-col gap-1">
  <span>Export and import icon settings:</span>
  <textarea rows=10 class="w-full text-white outline-none py-2 px-3 font-mono bg-neutral-700 rounded-lg" onchange={importSettings} bind:value={settings}></textarea>
</div>