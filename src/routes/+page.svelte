<script lang="ts">
	import Header from './Header.svelte';
	let name = $state('Scott');
	let status: 'OPEN' | 'CLOSED' = $state('OPEN');
	function toggle() {
		status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
	}
</script>

<Header {name} />

<p>The store is now {status}</p>

<button onclick={toggle}>Toggle Status</button>
