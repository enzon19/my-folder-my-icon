<script>
  import { dropzone } from "@sveu/actions";
	import { icon } from '$lib/icon.svelte.js';
  import Range from "./Range.svelte";
  import ColorPicker from "./ColorPicker.svelte";
  import Button from "./Button.svelte";

  function fileUpload(data) {
    const receivedFile = data.detail[0];
    if (receivedFile && receivedFile.type.startsWith("image/")) {
      const reader = new FileReader();

      reader.onload = () => {
        const img = new Image();
        img.onload = () => {
          icon.image.sizeHeight = img.naturalHeight;
          icon.image.sizeWidth = img.naturalWidth;
          icon.image.originalHeight = img.naturalHeight;
          icon.image.originalWidth = img.naturalWidth;
          if (Math.floor(icon.image.originalHeight) === 24 & Math.floor(icon.image.originalWidth) === 24) icon.image.scale = 1865;
          updateSize();
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

  // Manage image
  function updateSize() {
    icon.image.sizeWidth = (icon.image.originalWidth * icon.image.scale) / 100;
    icon.image.sizeHeight = (icon.image.originalHeight * icon.image.scale) / 100;
    centerImageX();
    centerImageY();
  }

  function centerImageX() {
    icon.image.positionX = (1000 - icon.image.sizeWidth) / 2;
  }

  function centerImageY() {
    const elementStartY = 257; // Starting Y position of the element
    const elementHeight = 546; // Assuming the element's total height fills the remaining space
    const elementCenterY = elementStartY + elementHeight / 2; // Center of the element

    icon.image.positionY = elementCenterY - icon.image.sizeHeight / 2; // Center the image relative to the element
  }

  function removeImage() {
    icon.image = {
      url: null,
      type: "",
      color1: "#c99101",
      color2: "#a26d01",
      positionX: 0,
      positionY: 0,
      sizeWidth: 1000,
      sizeHeight: 1000,
      originalWidth: 1000,
      originalHeight: 1000,
      scale: 100,
    };
  }

  function removeColors() {
    icon.image.color1 = null;
    icon.image.color2 = null;
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
  </div>
  <input type="file" bind:this={fileInput} class="hidden" onchange={handleFileChange} accept="image/*"/>
{:else}
  <div class="flex flex-col gap-2">
    <div class="flex flex-row gap-2">
      <div class="flex flex-col gap-2 w-full">
        <ColorPicker label="Icon, Color 1" id="iconColor1" bind:value={icon.image.color1}/>
        <ColorPicker label="Icon, Color 2" id="iconColor2" bind:value={icon.image.color2}/>
      </div>
      <Button onclick={removeColors}>
        No color
      </Button>
    </div>
    <div class="flex flex-row gap-2">
      <Range label="X Position:" id="x" max=1000 bind:value={icon.image.positionX}/>
      <Button onclick={centerImageX}>
        Center
      </Button>
    </div>
    <div class="flex flex-row gap-2">
      <Range label="Y Position:" id="y" max=1000 bind:value={icon.image.positionY}/>
      <Button onclick={centerImageY}>
        Center
      </Button>
    </div>
    <Range label="Scale:" id="scale" max=5000 bind:value={icon.image.scale} oninput={updateSize}/>
    <Range label="Width:" id="width" max={icon.image.originalHeight * 4} bind:value={icon.image.sizeWidth}/>
    <Range label="Height:" id="height" max={icon.image.originalHeight * 4} bind:value={icon.image.sizeHeight}/>
    <button class="bg-red-800/50 rounded-lg border shadow px-4 py-2 border-red-900" onclick={removeImage}>
      Remove image
    </button>
  </div>
{/if}