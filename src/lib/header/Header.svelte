<script>
	import LogoSVG from '../icons/Logo.svelte';
</script>

<section>
	<div class="wrapper">
		<nav>
			<div class="nav__left-side">
				<a href="/" class="nav__router-link">Recipes</a>
				<LogoSVG />
			</div>
			<div class="nav__right-side">
				<a href="/images" class="nav__router-link">Demo images</a>
				<a href="/text" class="nav__router-link">Demo text</a>
				<a href="/buttons" class="nav__router-link">Demo buttons</a>
			</div>
		</nav>
	</div>
</section>

<style>
	.nav__left-side {
		display: flex;
		align-items: center;
		font-size: 25px;
	}

	.nav__right-side {
		font-size: 15px;
		display: flex;
		align-items: center;
		gap: 15px;
	}

	.nav__router-link {
		margin-right: 5px;
		color: #ed6a5a;
		text-decoration: none;
		font-weight: 600;
	}

	nav {
		display: flex;
		justify-content: space-between;
		align-items: center;
		max-width: 1280px;
		margin: 0 auto;
		padding: 30px;
	}

	.wrapper {
		background-color: antiquewhite;
	}
</style>
