<script>
  import Preview from '$lib/components/Preview.svelte';
  import Colors from '$lib/components/Colors.svelte';
  import Image from '$lib/components/Image.svelte';
  import Export from '$lib/components/Export.svelte';

	import { icon } from '$lib/icon.svelte.js';

  let tab = $state('folderColor');
</script>

<h1 class="text-3xl font-bold text-center mx-auto">My Folder, My Icon</h1>
<div class="text-center text-xl mt-1">Create your own Windows 11-like directory icons using an editor!</div>
<div class="my-4 bg-yellow-500/30 border border-yellow-800 shadow p-4 rounded-lg">
  You can download pre-made icons in <a href="https://icon11-community.github.io/icons/" class="font-bold underline text-yellow-200" target="_blank">Folder11</a>. Those icons weren't created using this tool, but I'm sharing the project because the folder illustration I use here was based on their template. Full credits to the Folder11 Community. Be sure to check out their website!
</div>
<div class="flex flex-col md:flex-row gap-4 md:items-center">
  <div class="md:w-1/2 h-max relative flex aspect-square items-center justify-center">
    <div class="max-w-96 max-h-96 mx-auto relative z-10">
      <Preview colors={icon.colors} image={icon.image}/>
    </div>
    <div class="grid-background absolute top-0 left-0 w-full h-full"></div>
  </div>  
  <div class="md:w-1/2">
    <div class="rounded-xl p-1 bg-neutral-800 grid grid-cols-3 gap-1 mb-4">
      <button class="shadow p-2 rounded-lg" class:bg-neutral-600={tab === 'folderColor'} onclick={() => tab = 'folderColor'}>
        Colors
      </button>
      <button class="shadow p-2 rounded-lg" class:bg-neutral-600={tab === 'folderImage'} onclick={() => tab = 'folderImage'}>
        Image
      </button>
      <button class="shadow p-2 rounded-lg" class:bg-neutral-600={tab === 'export'} onclick={() => tab = 'export'}>
        <span class="hidden sm:inline">Export & Import</span>
        <span class="sm:hidden">Export</span>
      </button>
    </div>
    {#if tab === 'folderColor'}
      <Colors/>
    {:else if tab === 'folderImage'}
      <Image/>
    {:else if tab === 'export'}
      <Export/>
    {/if}
  </div>
</div>

<style>
  .grid-background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: 
      linear-gradient(90deg, rgba(80, 80, 80, 0.4) 1px, transparent 1px),
      linear-gradient(180deg, rgba(80, 80, 80, 0.4) 1px, transparent 1px);
    background-size: 30px 30px;
    background-position: center;
    z-index: 0; /* Ensure grid is behind the Preview */
  }

  .grid-background::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle, transparent 10%, rgb(23, 23, 23) 70%);
    pointer-events: none;
  }
</style>
