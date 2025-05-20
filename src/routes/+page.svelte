<script lang="ts">
	import Forms from './Forms.svelte';
	import Header from './Header.svelte';
	let name = $state('Scott');
</script>

<Header {name} fake_name="asdas" />

<Forms />
