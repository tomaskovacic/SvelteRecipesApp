<script>
	import MinutesSVG from '../../../lib/icons/Minutes.svelte';
	import ServingsSVG from '../../../lib/icons/Servings.svelte';
	import LikesSVG from '../../../lib/icons/Likes.svelte';
	import HealthSVG from '../../../lib/icons/Health.svelte';
	import { onMount } from 'svelte';

    import { page } from '$app/stores';

	let recipe = [];
	let recipeIngredients = [];
    let recipeAnalyzedInstructions = [];
    let recipeId = 10000;

    recipeId = $page.url.pathname.split('/')[2];

	onMount(async function () {
		const response = await fetch(
			'https://api.spoonacular.com/recipes/' +
				recipeId +
				'/information?apiKey=c28ec5bb4e7d4524810b868ae1b00baa '
		);
		const data = await response.json();
		recipe = data;
		recipeIngredients = recipe.extendedIngredients;
        recipeAnalyzedInstructions = recipe.analyzedInstructions;
	});
</script>

<div class="main-wrapper">
	<div class="breadcrumbs">
		<a href="/" class="breadcrumbs-previous">Home</a>
		<p class="seperator">></p>
		<p class="breadcrumbs-active">{recipe.title}</p>
	</div>
	<div class="summary-wrapper">
		<img class="image" alt="img" src={recipe.image} />
		<div>
			<h1 class="title">{recipe.title}</h1>
			<div class="info-wrapper">
				<div class="flex">
					<MinutesSVG />
					<p class="ingredients">{recipe.readyInMinutes} minutes</p>
				</div>
				<div class="flex">
					<ServingsSVG />
					{#if recipe.servings > 1}
						<p class="ingredients">
							{recipe.servings} people
						</p>
					{:else}
						<p class="ingredients">{recipe.servings} person</p>
					{/if}
				</div>
				<div class="flex">
					<LikesSVG />
					<p class="ingredients">{recipe.aggregateLikes} likes</p>
				</div>
				<div class="flex">
					<HealthSVG />
					<p class="ingredients">{recipe.healthScore} score</p>
				</div>
			</div>
			<p class="text">{@html recipe.summary}</p>
		</div>
	</div>
	<div class="details-wrapper">
		<div class="details-inner-wrapper">
			<div class="left-side">
				<div>
					<h3 class="bold-title bold-title2">Instructions</h3>
					{#each recipeAnalyzedInstructions as instruction}
						<div class="ingredients">
							{#each instruction.steps as instruction2}
								<div class="ingredients">
									<div class="ingredients-wrapper">
										<span class="big-number">{instruction2.number}</span>
										<span class="ingredients-text">{instruction2.step}</span>
									</div>
								</div>
							{/each}
						</div>
					{/each}
				</div>
			</div>

			<div class="right-side">
				<div>
					<h3 class="bold-title">Ingredients</h3>
					{#each recipeIngredients as ingredients}
						<p class="ingredients">
							○ {ingredients.original}
						</p>
					{/each}
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.text :deep(a),
	.breadcrumbs-previous {
		text-decoration: none;
		color: #ed6a5a;
	}

	.breadcrumbs {
		display: flex;
		color: rgb(158, 158, 158);
		padding-top: 30px;
		padding-bottom: 0;
	}

	.seperator {
		margin: 0 10px;
	}

	.info-wrapper {
		display: flex;
		gap: 30px;
		margin-bottom: 20px;
	}

	.ingredients-wrapper {
		padding: 10px 0;
	}

	.ingredients-text {
		line-height: 35px;
	}

	.big-number {
		font-size: 24px;
		font-weight: 600;
		color: #ed6a5a;
		margin-right: 10px;
	}

	.bold-title {
		margin: 0 0 20px 0;
		font-weight: 600;
		font-size: 23px;
		color: #333333;
	}

	.bold-title2 {
		margin-top: 30px;
	}

	.ingredients {
		line-height: 35px;
	}

	.flex {
		display: flex;
		align-items: center;
		font-size: 17px;
		color: #333333;
	}

	.text {
		color: rgb(158, 158, 158);
		line-height: 30px;
	}

	.image {
		max-width: 500px;
		max-height: 500px;
	}

	.title {
		font-weight: 600;
		color: white;
		padding-left: 10px;
		margin-bottom: 15px;
		background: #ed6a5a;
	}

	.summary-wrapper {
		display: flex;
		gap: 50px;
	}

	.details-wrapper {
		background-color: #f7f7f7;
	}

	.details-inner-wrapper {
		display: flex;
		gap: 50px;
		margin-top: 50px;
	}

	.main-wrapper {
		margin-top: 0px;
		margin-bottom: 70px;
	}

	.left-side {
		width: 100%;
	}

	.right-side {
		width: 50%;
		padding: 30px;
		box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
		border-radius: 15px;
		height: fit-content;
		background-color: antiquewhite;
	}
</style>
