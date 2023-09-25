<script>
	import { onMount } from "svelte";
	import ThumbsDown from "./lib/ThumbsDown.svelte";
	import Heart from "./lib/Heart.svelte";
	import { pizzaList } from "./lib/pizzas.js";

	const sleep = (ms = 2000) => new Promise((r) => setTimeout(r, ms));

	let currentPizza = {
		name: "",
		image: "",
	};

	let pizzas = pizzaList;
	let lovedPizzas = [];
	let showingPizza = true;
	let appearing = true;
	let bad = false;
	let loved = false;

	onMount(async () => {
		await showPizza();
	});

	async function showPizza() {
		await sleep(400);

		bad = false;
		loved = false;
		appearing = true;

		currentPizza = pizzas[Math.floor(Math.random() * pizzas.length)];

		await sleep(400);

		appearing = false;
	}

	async function thumbsDownClicked() {
		bad = true;

		let indexToRemove = pizzas.findIndex((pizza) => {
			return pizza.name === currentPizza.name;
		});
		pizzas.splice(indexToRemove, 1);

		if (pizzas.length == 0) {
			pizzas = structuredClone(lovedPizzas);
			lovedPizzas = [];
		}

		await showPizza();
	}

	async function loveClicked() {
		loved = true;

		let indexToRemove = pizzas.findIndex((pizza) => {
			return pizza.name === currentPizza.name;
		});

		lovedPizzas.push(pizzas[indexToRemove]);
		pizzas.splice(indexToRemove, 1);

		if (pizzas.length == 0) {
			pizzas = structuredClone(lovedPizzas);
			lovedPizzas = [];
		}

		await showPizza();
	}
</script>

<h1>Pizza Tinder</h1>

<div class="app">
	<ThumbsDown on:click={thumbsDownClicked} />
	{#if showingPizza}
		<img
			src={currentPizza.image}
			alt={currentPizza.name}
			class="pizza"
			class:appearing
			class:bad
			class:loved
		/>
	{/if}
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
		transition: all 0.4s ease;
	}

	.pizza.appearing {
		opacity: 0;
		transform: scale(0.1);
	}

	.pizza.bad {
		opacity: 0;
		transform: translateX(-48rem) scale(0.1);
	}

	.pizza.loved {
		opacity: 0;
		transform: translateX(48rem) scale(0.1);
	}
</style>
