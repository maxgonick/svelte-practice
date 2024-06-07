<script lang="ts">
	import xSvg from '$lib/assets/x.svg';
	import ySvg from '$lib/assets/o.svg';
	import { tick } from 'svelte';
	let playerTurn = true;

	let board: number[][] = [
		[-1, -1, -1],
		[-1, -1, -1],
		[-1, -1, -1]
	];

	let hoverMap: boolean[][] = [
		[false, false, false],
		[false, false, false],
		[false, false, false]
	];

	const handleClick = (row: number, col: number, e: Event): void => {
		board[row][col] = playerTurn ? 0 : 1;
		board = board;
		playerTurn = !playerTurn;
	};

	const handleMouseEnter = (row: number, col: number): void => {
		if (board[row][col] !== -1) return;
		hoverMap[row][col] = true;
		hoverMap = hoverMap;
	};

	const handleMouseLeave = (row: number, col: number): void => {
		if (board[row][col] !== -1) return;
		hoverMap[row][col] = false;
		hoverMap = hoverMap
	}

</script>

<div class="board-wrapper">
	<div class="board">
		{#each Array.from({ length: 3 }, (_, i) => i) as row}
			{#each Array.from({ length: 3 }, (_, j) => j) as col}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div
					class="cell"
					on:click|stopPropagation={(e: Event) => {
						handleClick(row, col, e);
					}}
					on:mouseenter|stopPropagation={() => {
						handleMouseEnter(row, col);
					}}
					on:mouseleave|stopPropagation={() => {
						handleMouseLeave(row, col);
					}}
					on:focus={() => {}}
				>
					<!-- {#if board[row][col] === 0}
						<img src={xSvg} alt="icon" />
					{:else if board[row][col] === 1}
						<img src={ySvg} alt="icon" />
					{/if} -->
					{#if hoverMap[row][col] === true}
						<img src={playerTurn ? xSvg : ySvg} alt="icon" style="opacity: 0.75;" />
					{/if}
				</div>
			{/each}
		{/each}
	</div>
	<div class="border" style="height: 100%; width: 0.5rem; top: 0; left: 9rem"></div>
	<div class="border" style="height: 100%; width: 0.5rem; top: 0; left: 18rem"></div>
	<div class="border" style="width: 100%; height: 0.5rem; top: 9rem; left: 0"></div>
	<div class="border" style="width: 100%; height: 0.5rem; top: 18rem; left: 0"></div>
</div>

<style>
	.board {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-template-rows: repeat(3, 1fr);
		height: 27rem;
		width: 27rem;
	}

	.cell {
		color: white;
		text-align: center;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.border {
		position: absolute;
		background-color: rgb(64 64 64);
	}

	.board-wrapper {
		position: relative;
	}
</style>
