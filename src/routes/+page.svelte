<script lang="ts">
	import enterSvg from '$lib/assets/enter.svg';
	import { goto } from '$app/navigation';
	const handleKeyDown = (e: KeyboardEvent): void => {
		if (e.key !== 'Enter') {
			return;
		}
		goto('/game');
	};
</script>

<svelte:window on:keydown={handleKeyDown} />

<main>
	<div class="title">tic tac toe</div>
	<div class="play">
		<a href="/game"><button class="playButton">Play a Game</button></a>
		<img alt="enter" src={enterSvg} class="playImg" />
	</div>
</main>

<style>
	main {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100vh;
		flex-direction: column;
		background-color: rgb(36, 36, 36);
	}
	.title {
		font-size: 6rem;
		font-weight: 700;
		color: white;
	}

	.play {
		gap: 1rem;
		display: flex;
		margin-top: 5%;
	}
	.playButton {
		justify-self: center;
		background-color: rgba(146, 64, 14, 0.5);
		border: rgb(146 64 14);
		border-radius: 12px;
		padding: 0.5rem 1rem;
		color: white;
		transition: background-color 0.25s ease-in-out;
	}

	.playButton:hover {
		background-color: rgba(146, 64, 14, 0.75);
	}

	.playImg {
		width: 2rem;
		height: 2rem;
	}
</style>
