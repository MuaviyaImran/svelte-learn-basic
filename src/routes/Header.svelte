<script lang="ts">
	let { name, fake_name }: { name: string; fake_name?: string } = $props();
	let full_name = $derived(name + ' ' + 'Marsh');
</script>

<h1 class="">Hello {name}</h1>
<h2>{name.replace('t', 'x')}</h2>
<h2>{full_name}</h2>
<h3>{fake_name}</h3>
<input type="text" bind:value={name} />
