<script lang="ts">
	import Board from '$comp/Board.svelte';
	import { writable } from 'svelte/store';
	import type { Writable } from 'svelte/store';

	const playerTurn: Writable<boolean> = writable(true);
	const record: Writable<number[]> = writable([0, 0]);

	enum Winner {
		No = 0,
		Player = 1,
		Computer = 2
	}

	const winnerStore: Writable<Winner> = writable(Winner.No);
</script>

<div class="main">
	<nav>
		<div class="record">
			<svg
				width="11"
				height="15"
				viewBox="0 0 11 15"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
			>
				<path
					fill-rule="evenodd"
					clip-rule="evenodd"
					d="M5.5 0.875C3.49797 0.875 1.875 2.49797 1.875 4.5C1.875 6.15288 2.98124 7.54738 4.49373 7.98351C3.2997 8.12901 2.27557 8.55134 1.50407 9.31167C0.522165 10.2794 0.0250244 11.72 0.0250244 13.5999C0.0250244 13.8623 0.237695 14.0749 0.500025 14.0749C0.762365 14.0749 0.975024 13.8623 0.975024 13.5999C0.975024 11.8799 1.42786 10.7206 2.17091 9.9883C2.91536 9.25463 4.02674 8.87499 5.49995 8.87499C6.97317 8.87499 8.0846 9.25463 8.8291 9.98831C9.5721 10.7206 10.025 11.8799 10.025 13.5999C10.025 13.8623 10.2376 14.0749 10.5 14.0749C10.7623 14.075 10.975 13.8623 10.975 13.6C10.975 11.72 10.4778 10.2794 9.4959 9.31166C8.7244 8.55135 7.70026 8.12903 6.50626 7.98352C8.01871 7.5474 9.125 6.15289 9.125 4.5C9.125 2.49797 7.50203 0.875 5.5 0.875ZM2.825 4.5C2.825 3.02264 4.02264 1.825 5.5 1.825C6.97736 1.825 8.175 3.02264 8.175 4.5C8.175 5.97736 6.97736 7.175 5.5 7.175C4.02264 7.175 2.825 5.97736 2.825 4.5Z"
					fill="#F5F5F5"
				></path>
			</svg>
			{$record[0]} |
			<svg
				width="17"
				height="14"
				viewBox="0 0 17 14"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
			>
				<path d="M16 7H1" stroke="#F5F5F5" stroke-linecap="round" stroke-linejoin="round"></path>
				<path
					d="M3.5875 1.8325L1 7V11.5C1 11.8978 1.15804 12.2794 1.43934 12.5607C1.72064 12.842 2.10218 13 2.5 13H14.5C14.8978 13 15.2794 12.842 15.5607 12.5607C15.842 12.2794 16 11.8978 16 11.5V7L13.4125 1.8325C13.2883 1.58259 13.0969 1.37228 12.8597 1.22521C12.6226 1.07814 12.3491 1.00015 12.07 1H4.93C4.65094 1.00015 4.37745 1.07814 4.14028 1.22521C3.90312 1.37228 3.71168 1.58259 3.5875 1.8325Z"
					stroke="#F5F5F5"
					stroke-linecap="round"
					stroke-linejoin="round"
				></path>
				<path d="M5 10H5.01" stroke="#F5F5F5" stroke-linecap="round" stroke-linejoin="round"></path>
				<path d="M9 10H9.01" stroke="#F5F5F5" stroke-linecap="round" stroke-linejoin="round"></path>
			</svg>

			{$record[1]}
		</div>
	</nav>
	<div class="body">
		<div class="turn">
			{#if $winnerStore === Winner.Player}
				Player Wins!
			{:else if $winnerStore === Winner.Computer}
				Opponent Turn
			{:else if $playerTurn === true}
				Player Turn
			{:else}
				Computer Turn
			{/if}
		</div>
		<Board {playerTurn} {record} {winnerStore} />
	</div>
</div>

<style>
	.main {
		height: 100vh;
		background-color: rgb(36, 36, 36);
		display: flex;
		flex-direction: column;
		padding: 1rem 0.5rem;
	}
	.body {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		gap: 2rem;
		flex-grow: 1;
	}

	.turn {
		background-color: rgba(146, 64, 14, 0.5);
		color: white;
		padding: 0.25rem 1rem;
		border-radius: 1rem;
		border: 1px solid rgb(146, 64, 14);
		min-width: 10rem;
		text-align: center;
	}

	nav {
		display: flex;
		justify-content: end;
	}

	.record {
		background-color: rgba(146, 64, 14, 0.5);
		color: white;
		padding: 0.25rem 1rem;
		border-radius: 1rem;
		border: 1px solid rgb(146, 64, 14);
		display: flex;
		justify-content: center;
		gap: 0.5rem;
		align-items: center;
		margin-left: auto;
		min-width: 5%;
		text-align: center;
	}
</style>
