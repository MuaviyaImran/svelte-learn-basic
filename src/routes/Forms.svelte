<script lang="ts">
	let formState = $state({
		name: '',
		birthday: '',
		step: 0,
		error: ''
	});
</script>

<main>
	<p>Step : {formState.step + 1}</p>

	{#if formState.step == 0}
		<div>
			<label for="name">Your Name</label>
			<input type="text" id="name" bind:value={formState.name} placeholder="Enter your name" />
		</div>
		<button
			onclick={() => {
				if (formState.name !== '') {
					formState.step += 1;
					formState.error = '';
				} else {
					formState.error = 'Please enter your name';
				}
			}}
		>
			Next
		</button>
	{:else if formState.step == 1}
		<div>
			<label for="name">Your Birthday</label>
			<input
				type="date"
				id="bday"
				bind:value={formState.birthday}
				placeholder="Enter your birthday"
			/>
		</div>
		<button
			onclick={() => {
				if (formState.birthday !== '') {
					formState.step += 1;
					formState.error = '';
				} else {
					formState.error = 'Please enter your birthday';
				}
			}}
		>
			Next
		</button>
	{:else if formState.step == 2}
		<p class="success">Form Submitted Successfully</p>
	{/if}
	{#if formState.error !== ''}
		<p class="error">{formState.error}</p>
	{/if}
</main>

<style>
	.error {
		color: red;
		font-size: 14px;
	}
	.success {
		color: green;
	}
</style>
