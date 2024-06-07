<script lang="ts">
    let playerTurn = true;



	const handleClick = (event: Event) => {
        if (playerTurn) {
            event.target
        }
    };
</script>

<div class="board-wrapper">
	<div class="board">
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="cell" on:click={handleClick}><img alt="icon"/></div>
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
	}

	.border {
		position: absolute;
		/* background-color: rgb(64 64 64); */
		background-color: red;
	}

	.board-wrapper {
		position: relative;
	}
</style>
