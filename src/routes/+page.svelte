<script>
	import MinutesSVG from '../lib/icons/Minutes.svelte';
	import ServingsSVG from '../lib/icons/Servings.svelte';
	import { onMount } from 'svelte';

	let recipes = [];

	onMount(async function () {
		const response = await fetch(
			'https://api.spoonacular.com/recipes/complexSearch?number=12&addRecipeNutrition=true&apiKey=bcbfd5f464b14b9784d33e9aac512519'
		);
		const data = await response.json();
		recipes = data.results;
	});

  
</script>

<section>
	<div class="text-wrapper">
		<h1>BEST FOOD FOR YOUR TASTE</h1>
	</div>
	<div class="wrapper">
		<h3>Recipes</h3>
		<div class="div__hr" />
	</div>
	<div class="recipes">
		{#each recipes as recipe}
			<div class="recipes__item">
				<a class="router-link" href={`/recipe/${recipe.id}`}>
					<div class="recipes__item-left-side">
						<img class="recipes__item-image" alt="img" src={recipe.image} />
					</div>
					<div class="recipes__item-right-side">
						<div>
							<h2 class="recipes__item-title">{recipe.title}</h2>
							<div class="recipes__item-minutes-wrapper">
								<MinutesSVG class="minutes" />
								<p class="recipes__item-minutes">
									{recipe.readyInMinutes} min •
								</p>
								<ServingsSVG class="servings" />
								<p class="recipes__item-minutes">{recipe.servings}</p>
							</div>
						</div>
						<div class="diet-wrapper">
							<div class="diet">
								{#each recipe.diets as diet}
									<div class="diet-item">{diet}</div>
								{/each}
							</div>
						</div>
					</div>
				</a>
			</div>
		{/each}
	</div>
</section>

<style>
	.servings {
		margin-right: 0 !important;
	}

	.minutes {
		margin-right: 0 !important;
	}

	.wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
		flex-flow: column;
	}

	.diet-item {
		margin-right: 10px;
		color: #999;
		border: 1px solid #999;
		border-radius: 25px;
		padding: 1px 4px;
		margin: 3px;
	}

	.diet {
		display: inline-block;
	}

	.diet-wrapper {
		display: inline-block;
		font-size: 12px;
		text-decoration: none;
		color: #333;
	}

	.active {
		background: #ed6a5a;
		color: white;
	}

	button:hover {
		background-color: #d8d8d8;
	}

	.text-wrapper {
		margin-bottom: 50px;
		background: #ed6a5a;
		color: white;
		font-weight: bold;
		height: 60px;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.router-link {
		width: 100%;
		height: 100%;
		display: flex;
		text-decoration: none;
	}

	.recipes {
		display: flex;
		flex-wrap: wrap;
		gap: 20px;
		margin-bottom: 60px;
	}

	.recipes__item-right-side {
		display: flex;
		padding: 15px 20px 15px 0;
		flex-flow: column;
		justify-content: space-around;
	}

	.recipes__item-left-side {
		width: 51%;
		padding: 20px;
		display: flex;
		align-items: center;
	}

	.recipes__item {
		display: flex;
		width: 385px;
		height: 200px;
		box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
		border-radius: 15px;
	}

	.recipes__item:hover {
		box-shadow: 0px 8px 15px rgba(224, 157, 130, 0.52);
		cursor: pointer;
	}

	.recipes__item-image {
		width: 120px;
		height: 120px;
		border-radius: 50%;
	}

	.recipes__item-minutes-wrapper {
		display: flex;
		align-items: center;
		margin-top: 10px;
	}

	.recipes__item-title {
		font-weight: 600;
		color: #333333;
		font-size: 16px;
	}

	.recipes__item-minutes {
		font-weight: 500;
		color: #858585;
		margin-left: 10px;
		margin-right: 10px;
	}

	h3 {
		font-size: 25px;
		color: #333333;
		display: flex;
		justify-content: center;
	}

	.div__hr {
		display: flex;
		width: 70px;
		height: 3px;
		background-color: #ed6a5a;
		justify-content: center;
		margin-top: 5px;
	}

	.recipes-nav {
		padding: 50px 100px 80px 100px;
		display: flex;
		justify-content: center;
		gap: 30px;
	}

	button {
		width: 150px;
		height: 30px;
		color: #333333;
		background-color: rgb(255, 255, 255);
		border: none;
		border-radius: 45px;
		box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
		text-transform: uppercase;
		cursor: pointer;
	}
</style>
