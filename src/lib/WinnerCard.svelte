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
	}

	.name {
		font-size: 7rem;
		font-weight: 700;
		margin: 2rem;
	}

	.image {
		aspect-ratio: 1 / 1;
		height: 60vh;
		border-radius: 2rem;
	}
</style>
