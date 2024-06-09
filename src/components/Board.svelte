<script lang="ts">
	import xSvg from '$lib/assets/x.svg';
	import oSvg from '$lib/assets/o.svg';
	import type { Writable } from 'svelte/store';
	enum Winner {
		No = 0,
		Player = 1,
		Computer = 2
	}
	export let playerTurn: Writable<boolean>;
	export let record: Writable<number[]>;
	export let winnerStore: Writable<Winner>;
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

	const resetBoard = (): void => {
		board = [
			[-1, -1, -1],
			[-1, -1, -1],
			[-1, -1, -1]
		];
		hoverMap = [
			[false, false, false],
			[false, false, false],
			[false, false, false]
		];
		return;
	};

	const handleClick = (row: number, col: number): void => {
		if (board[row][col] !== -1) return;
		board[row][col] = $playerTurn ? 0 : 1;
		board = board;
	};

	const handleMouseEnter = (row: number, col: number): void => {
		if (board[row][col] !== -1) return;
		hoverMap[row][col] = true;
		hoverMap = hoverMap;
	};

	const handleMouseLeave = (row: number, col: number): void => {
		if (board[row][col] !== -1) return;
		hoverMap[row][col] = false;
		hoverMap = hoverMap;
	};

	const getVerticalSlices = (arr: number[][]): number[][] => {
		//
		return arr[0].map((_, colIndex) => arr.map((row) => row[colIndex]));
	};
	const checkForWin = (board: number[][]): void => {
		if (
			board.every((arr: number[]) => {
				return arr.every((val: number) => {
					return val != -1;
				});
			})
		) {
			resetBoard();
			playerTurn.set(true);
			return;
		}

		//Check for Horizontal Wins
		for (const [index, row] of board.entries()) {
			if (row[0] !== -1 && row.every((val) => val == row[0])) {
				record.update((n) => {
					n[row[0]] += 1;
					return n;
				});
				winnerStore.set($playerTurn ? Winner.Player : Winner.Computer);
				resetBoard();
				playerTurn.set(!$playerTurn);
				return;
			}
		}
		//Check for Vertical Wins
		for (const col of getVerticalSlices(board)) {
			if (col[0] !== -1 && col.every((val) => val == col[0])) {
				record.update((n) => {
					n[col[0]] += 1;
					return n;
				});
				winnerStore.set($playerTurn ? Winner.Player : Winner.Computer);
				resetBoard();
				playerTurn.set(!$playerTurn);
				return;
			}
		}
		//Check Diagonal Wins
		if (
			board[1][1] !== -1 &&
			((board[0][0] === board[1][1] && board[1][1] === board[2][2]) ||
				(board[0][2] === board[1][1] && board[1][1] === board[2][0]))
		) {
			record.update((n) => {
				n[board[1][1]] += 1;
				return n;
			});
			winnerStore.set($playerTurn ? Winner.Player : Winner.Computer);
			resetBoard();
			playerTurn.set(!$playerTurn);
			return;
		}
		playerTurn.set(!$playerTurn);
		winnerStore.set(Winner.No);
	};

	$: checkForWin(board);
</script>

<div class="board-wrapper">
	<div class="board">
		{#each Array.from({ length: 3 }, (_, i) => i) as row}
			{#each Array.from({ length: 3 }, (_, j) => j) as col}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div
					class="cell"
					on:click|stopPropagation={() => {
						handleClick(row, col);
					}}
					on:mouseenter|stopPropagation={() => {
						handleMouseEnter(row, col);
					}}
					on:mouseleave|stopPropagation={() => {
						handleMouseLeave(row, col);
					}}
					on:focus={() => {}}
				>
					{#if board[row][col] === 0}
						<img src={xSvg} alt="icon" />
					{:else if board[row][col] === 1}
						<img src={oSvg} alt="icon" />
					{:else if hoverMap[row][col] === true}
						<img src={$playerTurn ? xSvg : oSvg} alt="icon" style="opacity: 0.75;" />
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

	.cell:hover {
		cursor: pointer;
	}

	.border {
		position: absolute;
		background-color: rgb(64 64 64);
	}

	.board-wrapper {
		position: relative;
	}
</style>
