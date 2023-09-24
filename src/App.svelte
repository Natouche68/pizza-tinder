<script>
	import { onMount } from "svelte";
	import ThumbsDown from "./lib/ThumbsDown.svelte";
	import Heart from "./lib/Heart.svelte";
	import { pizzaList } from "./lib/pizzas.js";

	let currentPizza = {
		name: "",
		image: "",
	};

	let pizzas = pizzaList;
	let lovedPizzas = [];

	onMount(() => {
		showPizza();
	});

	function showPizza() {
		currentPizza = pizzas[Math.floor(Math.random() * pizzas.length)];
	}

	function thumbsDownClicked() {
		let indexToRemove = pizzas.findIndex((pizza) => {
			return pizza.name === currentPizza.name;
		});
		pizzas.splice(indexToRemove, 1);

		if (pizzas.length == 0) {
			pizzas = structuredClone(lovedPizzas);
			lovedPizzas = [];
		}

		showPizza();
	}

	function loveClicked() {
		let indexToRemove = pizzas.findIndex((pizza) => {
			return pizza.name === currentPizza.name;
		});

		lovedPizzas.push(pizzas[indexToRemove]);
		pizzas.splice(indexToRemove, 1);

		if (pizzas.length == 0) {
			pizzas = structuredClone(lovedPizzas);
			lovedPizzas = [];
		}

		showPizza();
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
