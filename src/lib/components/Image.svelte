<script>
  import { dropzone } from "@sveu/actions";
	import { icon } from '$lib/icon.svelte.js';
  import Range from "./Range.svelte";

  function fileUpload(data) {
    const receivedFile = data.detail[0];
    if (receivedFile && receivedFile.type.startsWith("image/")) {
      const reader = new FileReader();

      reader.onload = () => {
        const img = new Image();
        img.onload = () => {
          icon.image.sizeHeight = img.naturalHeight;
          icon.image.sizeWidth = img.naturalWidth;
        };
        img.src = reader.result;
      };
      reader.readAsDataURL(receivedFile); // Read the file as a data URL

      const blob = new Blob([receivedFile], { type: receivedFile.type });
      const url = URL.createObjectURL(blob);

      icon.image.type = receivedFile.type;
      icon.image.url = url;
    } else {
      alert("Please select an image file.");
    }
  }
  
  // When user click
  let fileInput = $state();
  function handleClick() {
    fileInput.click();
  }
  function handleFileChange(event) {
    const files = event.target.files;
    if (files.length === 0) return;
    fileUpload({ detail: [files[0]] });
  }
</script>

{#if !icon.image.url}
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <div
    use:dropzone
    onfiles={fileUpload}
    class="bg-neutral-800/50 border-2 border-neutral-700 border-dashed p-16 text-center rounded-xl cursor-pointer"
    onclick={handleClick}
  >
    <div>Drop a image or icon here or click to select one</div>
    <div class="text-sm text-neutral-500 mt-2">Recommended: 1000 × 1000</div>
  </div>
  <input type="file" bind:this={fileInput} class="hidden" onchange={handleFileChange} accept="image/*"/>
{:else}
  <div class="flex flex-col gap-2">
    <Range label="X Position:" id="x" max=1000 bind:value={icon.image.positionX}/>
    <Range label="Y Position:" id="y" max=1000 bind:value={icon.image.positionY}/>
    <Range label="Width:" id="width" max=1000 bind:value={icon.image.sizeWidth}/>
    <Range label="Height:" id="height" max=1000 bind:value={icon.image.sizeHeight}/>
  </div>
{/if}