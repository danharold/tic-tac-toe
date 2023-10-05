<script lang="ts">
	import Tile from './Tile.svelte';
	import type { TileState, GameState } from '$lib/types';

	export let x: number = 3;
	export let y: number = 3;

	let grid: TileState[][] = Array.from({ length: x }, () =>
		new Array(y).fill('')
	);

	let state: GameState = 'X';

	$: {
		console.log(state);
	}

	function resetGame() {
		grid = Array.from({ length: x }, () => new Array(y).fill(''));
		state = 'X';
	}

	function validateMove(i: number, j: number) {
		let current = grid[i][j];
		let win: boolean = false;
		// vertical and horizontal
		if (grid[i][0] === grid[i][1] && grid[i][1] === grid[i][2]) {
			win = true;
		} else if (grid[0][j] === grid[1][j] && grid[1][j] === grid[2][j]) {
			win = true;
		}
		// diagonal
		if (i === j) {
			if (grid[0][0] === grid[1][1] && grid[1][1] === grid[2][2]) {
				win = true;
			}
		} else if (i + j === 2) {
			if (grid[0][2] === grid[1][1] && grid[1][1] === grid[2][0]) {
				win = true;
			}
		}
		if (win) {
			current === 'X' ? (state = 'X wins') : (state = 'O wins');
		}
	}

	function clickTile(i: number, j: number) {
		if (state === 'X') {
			if (grid[i][j] === '') {
				grid[i][j] = 'X';
				state = 'O';
				validateMove(i, j);
			}
		} else if (state === 'O') {
			if (grid[i][j] === '') {
				grid[i][j] = 'O';
				state = 'X';
				validateMove(i, j);
			}
		}
	}

	$: console.log(grid);
</script>

<div class="grid grid-flow-row gap-10 px-10 py-10">
	<div
		class="grid gap-3"
		style="grid-template-columns: repeat({x}, minmax(0, 1fr))"
	>
		{#each grid as rows, i}
			{#each rows as item, j}
				<Tile bind:state={grid[i][j]} on:tileClick={() => clickTile(i, j)} />
			{/each}
		{/each}
	</div>
	<div class="flex h-20 flex-col items-center">
		<p>{state}</p>
		{#if state === 'O wins' || state === 'X wins'}
			<button
				class="variant-ghost-tertiary btn relative mt-6"
				on:click={resetGame}>Play Again</button
			>
		{/if}
	</div>
</div>
