<script>
	document.title = 'SynonymR';
	let error;
	let curWord;

</script>

<main>
	<h1>SynonymR</h1>
	<div class="form">
		<input type="text" placeholder="Enter a word" bind:value={curWord}>
		<button>Find Synonym</button>
	</div>
	<p class="error">{error || ''}</p>
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
		background: rgb(0,67,68);
		background: linear-gradient(0deg, rgba(0,67,68,1) 0%, rgba(0,0,0,1) 100%);
		height: 100vh;
		padding-top: 5%;
		width: 100%;
	}

	h1 {
		color: #FFFFFF;
		font-size: 6em;
		font-weight: 100;
		margin: 0;
	}

	.form {
		display: flex;
		justify-content: space-between;
		margin-left: auto;
		margin-right: auto;
		margin-top: 5%;
		width: 30%;
	}

	input {
		width: 60%;
	}

	.error {
		color: red;
		margin-left: auto;
		margin-right: auto;
		text-align: left;
		width: 30%;
	}

</style>
