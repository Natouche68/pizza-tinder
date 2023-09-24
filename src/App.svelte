<script>
	import ThumbsDown from "./lib/ThumbsDown.svelte";
	import Heart from "./lib/Heart.svelte";
</script>

<h1>Pizza Tinder</h1>

<div class="app">
	<ThumbsDown />
	<img src="pizzas/pepperoni pizza.png" alt="Pepperoni Pizza" class="pizza" />
	<Heart />
</div>

<style>
	h1 {
		width: 90%;
		margin: 3rem 5%;
		border-bottom: solid 1px var(--discret-color);
		text-align: center;
		font-weight: 700;
		font-size: 4rem;
	}

	.app {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}

	.pizza {
		aspect-ratio: 1 / 1;
		height: 80vh;
		border-radius: 4rem;
	}
</style>
