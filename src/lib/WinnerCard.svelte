<script>
	export let pizzaName;
	export let imagePath;
</script>

<div class="winner-card">
	<div class="label">And the winner is...</div>
	<div class="name">
		{pizzaName}
	</div>
	<img src={imagePath} alt={pizzaName} class="image" />
</div>

<style>
	.winner-card {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
	}

	.label {
		font-size: 3rem;
		font-weight: 500;
		font-style: italic;
		color: var(--discret-color);
		animation: label-animation 1s ease 1s 1 normal both;
	}

	@keyframes label-animation {
		from {
			color: var(--text-color);
			transform: scale(2) translateY(8rem);
		}

		to {
			color: var(--discret-color);
			transform: scale(1) translateY(0);
		}
	}

	.name {
		font-size: 7rem;
		font-weight: 700;
		margin: 2rem;
		animation: name-animation 2s ease 2s 1 normal both;
	}

	@keyframes name-animation {
		from {
			opacity: 0;
			filter: blur(2rem);
		}

		to {
			opacity: 1;
			filter: blur(0);
		}
	}

	.image {
		aspect-ratio: 1 / 1;
		height: 60vh;
		border-radius: 2rem;
		animation: image-animation 2s ease 2s 1 normal both;
	}

	@keyframes image-animation {
		from {
			opacity: 0;
			transform: scale(0);
		}

		to {
			opacity: 1;
			transform: scale(1);
		}
	}
</style>
