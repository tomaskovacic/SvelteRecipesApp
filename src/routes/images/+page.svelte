<script>
	let number = 0;
	let current = '';

	function handleClick(param) {
		number = param;
	}
</script>

<div class="text-wrapper">
	<h1>DEMO IMAGES</h1>
</div>
<div class="main-wrapper">
	<div class="nav">
		<button
			on:click|preventDefault={handleClick.bind(this, 10)}
			class={current === '10' ? 'i-am-active' : ''}
			on:click={() => (current = '10')}>10</button
		>
		<button
			on:click|preventDefault={handleClick.bind(this, 100)}
			class={current === '100' ? 'i-am-active' : ''}
			on:click={() => (current = '100')}>100</button
		>
		<button
			on:click|preventDefault={handleClick.bind(this, 1000)}
			class={current === '1000' ? 'i-am-active' : ''}
			on:click={() => (current = '1000')}>1000</button
		>
		<button
			on:click|preventDefault={handleClick.bind(this, 10000)}
			class={current === '10000' ? 'i-am-active' : ''}
			on:click={() => (current = '10000')}>10000</button
		>
		<button
			on:click|preventDefault={handleClick.bind(this, 100000)}
			class={current === '100000' ? 'i-am-active' : ''}
			on:click={() => (current = '100000')}>100000</button
		>
	</div>
	{#each { length: number } as _}
		<img alt="img" src="https://spoonacular.com/recipeImages/715497-556x370.jpg" />
	{/each}
</div>

<style>
	.main-wrapper {
		max-width: 1280px;
		margin: 0 auto;
		padding: 30px;
	}

	.text-wrapper {
		margin-bottom: 0;
		background: #ed6a5a;
		color: white;
		font-weight: bold;
		height: 60px;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.i-am-active {
		background: #ed6a5a;
		color: white;
	}

	.nav {
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
