<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import type { TileState } from '$lib/types';

	export let state: TileState = '';

	const dispatch = createEventDispatcher();

	function handleClick() {
		dispatch('tileClick');
	}
</script>

<button
	class="flex h-20 w-20 select-none items-center
	justify-center rounded-xl text-4xl font-bold outline-4 outline-white/10
	{state === '' && 'bg-tertiary-900/20 hover:outline'}
	{state === 'X' && 'pointer-events-none bg-primary-900'}
	{state === 'O' && 'pointer-events-none bg-secondary-900'}"
	on:click={handleClick}
>
	{state}
</button>
