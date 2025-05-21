<script lang="ts">
	let formState = $state({
		answers: {} as Record<string, any>,
		step: 0,
		error: ''
	});
	const QUESTIONS = [
		{
			question: "What's your name?",
			type: 'text',
			id: 'name'
		},
		{
			question: "What's your birthday?",
			type: 'date',
			id: 'birthday'
		},
		{
			question: "What's your favorite color? (Select one)",
			type: 'color',
			id: 'color'
		}
	];
	function nextStep(id: string) {
		if (formState.answers[id]) {
			formState.step += 1;
			formState.error = '';
		} else {
			formState.error = 'Please fill out the form field';
		}
	}
	// will be called when the component is mounted
	$effect(() => {
		console.log('Mounting Form');
		return () => {
			// will be called when the component is unmounted
			// before effect re runs
			console.log('Unmounting Form');
		};
	});

	$effect(() => {
		// This effect will run whenever formState.step changes
		console.log('Form State Changed', formState.step);
		// DON'T create state based off other state, in effect
		// use $derived() instead
		return () => {
			// Cleanup code if needed
			console.log('before Form State Changed', formState.step);
		};
	});

	// Its a good practice to use $inspect() to see the state of the store and debugging
	$inspect(formState.step);
</script>

<main class="table">
	{#if formState.step === QUESTIONS.length}
		<p class="success">Thank You...! Form submitted successfully!</p>
	{:else}
		<p>Step : {formState.step + 1}</p>
	{/if}

	{#each QUESTIONS as { question, id, type }, index (id)}
		{#if index === formState.step}
			{@render formStep({ question, type, id })}
		{/if}
	{/each}

	{#if formState.error !== ''}
		<p class="error">{formState.error}</p>
	{/if}
</main>

{#snippet formStep({ question, type, id }: { question: string; type: string; id: string })}
	<article>
		<div>
			<label for={id}>{question}</label>
			<input {type} {id} bind:value={formState.answers[id]} />
		</div>
		{#if formState.step === QUESTIONS.length - 1}
			<button onclick={() => nextStep(id)}>Submit</button>
		{:else}
			<button onclick={() => nextStep(id)}>Next</button>
		{/if}
	</article>
{/snippet}

<style>
	.error {
		color: red;
		font-size: 14px;
	}
	.success {
		color: green;
	}
	.table {
		display: table;
		width: 100%;
		border: 1px solid #ccc;
		margin: 20px 0;
		padding: 15px;
	}
</style>
