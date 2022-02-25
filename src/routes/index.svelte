<script>
	import Spinner from '../components/Spinner.svelte';
	import { onMount } from 'svelte';
	let data;

	const getAdvice = async () => {
		data = undefined;
		fetch('https://api.adviceslip.com/advice')
			.then((response) => response.json())
			.then((res) => {
				data = res;
			})
			.catch((error) => {
				console.log(error);
				return {};
			});
	};

	onMount(getAdvice);
</script>

<div class="w-screen h-screen bg-dgb flex flex-col justify-center items-center px-8">
	{#if data === undefined}
		<Spinner />
	{:else}
		<div
			class="bg-gb text-lc font-base text-center p-8 relative flex flex-col justify-center items-center gap-5 rounded-xl shadow-xl"
		>
			<p class="text-ng text-xs tracking-[0.2em] font-semibold">ADVICE #{data.slip.id}</p>
			<p class="text-2xl max-w-sm">
				"{data.slip.advice}"
			</p>

			<svg width="295" height="16" xmlns="http://www.w3.org/2000/svg" class="mb-9"
				><g fill="none" fill-rule="evenodd"
					><path fill="#4F5D74" d="M0 8h122v1H0zM173 8h122v1H173z" /><g
						transform="translate(138)"
						fill="#CEE3E9"
						><rect width="6" height="16" rx="3" /><rect x="14" width="6" height="16" rx="3" /></g
					></g
				></svg
			>

			<button class="p-4 bg-ng rounded-full absolute bottom-0 translate-y-1/2" on:click={getAdvice}>
				<svg width="24" height="24" xmlns="http://www.w3.org/2000/svg">
					<path
						d="M20 0H4a4.005 4.005 0 0 0-4 4v16a4.005 4.005 0 0 0 4 4h16a4.005 4.005 0 0 0 4-4V4a4.005 4.005 0 0 0-4-4ZM7.5 18a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Z"
						fill="#202733"
					/>
				</svg>
			</button>
		</div>
	{/if}
</div>
