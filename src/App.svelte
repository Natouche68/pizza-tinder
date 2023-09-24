<script>
	import { onMount } from "svelte";
	import ThumbsDown from "./lib/ThumbsDown.svelte";
	import Heart from "./lib/Heart.svelte";
	import { pizzas } from "./lib/pizzas.js";

	let currentPizza = {
		name: "",
		image: "",
	};

	onMount(() => {
		currentPizza = pizzas[Math.floor(Math.random() * pizzas.length)];
	});

	function thumbsDownClicked() {
		console.log("thumbs down clicked");
	}

	function loveClicked() {
		console.log("love clicked");
	}
</script>

<h1>Pizza Tinder</h1>

<div class="app">
	<ThumbsDown on:click={thumbsDownClicked} />
	<img src={currentPizza.image} alt={currentPizza.name} class="pizza" />
	<Heart on:click={loveClicked} />
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
