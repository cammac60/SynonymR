<script>
	export let name;
</script>

<main>
	<h1>Hello {name}!</h1>
</main>

<style>
	:global(body) {
		box-sizing: border-box;
		margin: 0;
		outline: none;
		padding: 0;
		text-align: center;
	}

	main {
		background: rgb(29,98,158);
		background: radial-gradient(circle, rgba(29,98,158,1) 0%, rgba(0,0,0,1) 100%);
		height: 100vh;
		width: 100%;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
		margin: 0;
	}

</style>
