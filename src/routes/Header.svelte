<script lang="ts">
	import { createState, ScottState } from './state.svelte';
	let { name, fake_name }: { name: string; fake_name?: string } = $props();
	let full_name = $derived(name + ' ' + 'Marsh');

	let status: 'OPEN' | 'CLOSED' = $state('OPEN');

	function onclick() {
		status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
	}
	const myState = createState();
	const myStateTwo = new ScottState();
</script>

<h1 class="">Hello {name}</h1>
<h2>{name.replace('t', 'x')}</h2>
<h2>{full_name}</h2>
<h3>{fake_name}</h3>

<button {onclick}>Toggle Status</button>
<p>The store is now {status}</p>

<input type="text" bind:value={name} />

<div>
	<p>Create State</p>
	<p>Function Base State</p>
	<button onclick={myState.up}>
		{myState.value}
	</button>
	<p>Class Base State</p>
	<button onclick={() => myStateTwo.up()}>
		{myStateTwo.value}
	</button>
</div>
