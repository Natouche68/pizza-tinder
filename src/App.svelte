<script>
	import { onMount } from "svelte";
	import ThumbsDown from "./lib/ThumbsDown.svelte";
	import Heart from "./lib/Heart.svelte";
	import WinnerCard from "./lib/WinnerCard.svelte";
	import { pizzaList } from "./lib/pizzas.js";

	const sleep = (ms = 2000) => new Promise((r) => setTimeout(r, ms));

	let currentPizza = {
		name: "",
		image: "",
	};

	let pizzas = pizzaList;
	let lovedPizzas = [];
	let showingPizza = false;
	let appearing = true;
	let bad = false;
	let loved = false;

	let message = "Round 1";
	let currentRound = 1;
	let isMessageAppearing = false;

	let hasWinner = false;

	onMount(async () => {
		await sleep(800);

		isMessageAppearing = true;

		await sleep(400);

		isMessageAppearing = false;

		showingPizza = true;

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
			await newRound();
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
			await newRound();
		}

		await showPizza();
	}

	async function newRound() {
		await sleep(400);

		pizzas = structuredClone(lovedPizzas);
		lovedPizzas = [];

		if (pizzas.length == 1) {
			hasWinner = true;
			currentPizza = pizzas[0];
		}

		currentRound++;
		message = `Round ${currentRound}`;

		showMessage();
	}

	async function showMessage() {
		isMessageAppearing = true;
		showingPizza = false;

		await sleep(400);

		isMessageAppearing = false;

		await sleep(1200);

		isMessageAppearing = true;

		await sleep(400);

		showingPizza = true;
		isMessageAppearing = false;
	}
</script>

<h1>Pizza Tinder</h1>

<div class="app">
	{#if hasWinner}
		<WinnerCard pizzaName={currentPizza.name} imagePath={currentPizza.image} />
	{:else}
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
		{:else}
			<div class="message" class:appearing={isMessageAppearing}>
				{message}
			</div>
		{/if}
		<Heart on:click={loveClicked} />
	{/if}
</div>

<style>
	h1 {
		width: 90%;
		margin: 3rem 5%;
		border-bottom: solid 1px var(--separation-color);
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

	.message {
		height: 80vh;
		width: 80vh;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 8rem;
		font-weight: 600;
		opacity: 1;
		transform: scale(1) translateY(0);
		transition: all 0.4s ease;
	}

	.message.appearing {
		opacity: 0;
		transform: scale(0.1) translateY(-16rem);
	}
</style>
