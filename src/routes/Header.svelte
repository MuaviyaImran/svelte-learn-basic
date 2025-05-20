<script lang="ts">
	let { name }: { name: string } = $props();
</script>

<h1 class="">Hello {name}</h1>
<h2>{name.replace('t', 'x')}</h2>
<input type="text" bind:value={name} />
