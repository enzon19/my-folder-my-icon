<script>
  import ColorPicker from "./ColorPicker.svelte";
	import { icon } from '$lib/icon.svelte.js';
</script>

<div class="flex flex-col gap-2">
  <ColorPicker label="Top" id="layer0color1" bind:value={icon.colors.layer0Color1}/>
  <ColorPicker label="Main, Color 1" id="layer2Color1" bind:value={icon.colors.layer2Color1}/>
  <ColorPicker label="Main, Color 2" id="layer2Color2" bind:value={icon.colors.layer2Color2}/>
  <ColorPicker label="Glow, Color 1" id="layer3Color1" bind:value={icon.colors.layer3Color1}/>
  <ColorPicker label="Glow, Color 2" id="layer3Color2" bind:value={icon.colors.layer3Color2}/>
  <ColorPicker label="Bottom, Color 1" id="layer4Color1" bind:value={icon.colors.layer4Color1}/>
  <ColorPicker label="Bottom, Color 2" id="layer4Color2" bind:value={icon.colors.layer4Color2}/>
</div>