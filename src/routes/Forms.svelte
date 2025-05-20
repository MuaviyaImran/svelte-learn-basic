<script lang="ts">
	let formState = $state({
		answers: {},
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
</script>

<main>
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
</style>
