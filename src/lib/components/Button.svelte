<script>
	let { children, onclick } = $props();
</script>

<button class="bg-neutral-800/50 rounded-lg border shadow px-4 border-neutral-800" {onclick}>
  {@render children()}
</button>  