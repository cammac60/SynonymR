<script>

	document.title = 'SynonymR';

	let error;
	let curWord;
	let foundWords = [];

	const fetchSyns = async () => {
		const url = `https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${curWord}?key=3d79f969-d355-4060-9017-28021b58745e`;
		const response = await fetch(url);
		if (!response.ok) {
			throw new Error('Error: The synonyms couldn\'t be found.')
		}
		const data = await response.json();
		return data;
	};

	const handleSubmit = async () => {
		try {
			const syns = await fetchSyns();
			console.log(syns);
		} catch(error) {
			console.log(error);
		}
	};

</script>

<main>

	<h1>SynonymR</h1>
	<div class="form">
		<input type="text" placeholder="Enter a word" bind:value={curWord}>
		<button on:click={handleSubmit}>Find Synonyms</button>
	</div>
	<p class="error">{error || ''}</p>
	<div class="word-wrapper">

	</div>

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
		overflow-x: scroll;
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
		outline: none;
		width: 60%;
	}

	.error {
		color: red;
		margin-left: auto;
		margin-right: auto;
		text-align: left;
		width: 30%;
	}

	button {
		cursor: pointer;
	}

	button:active {
		color: #FFFFFF;
		background: rgba(0,67,68,1);
	}

	.word-wrapper {
		color: #FFFFFF;
		display: grid;
		font-size: 2rem;
		grid-template-columns: repeat(4, 1fr);
		grid-column-gap: 20px;
		grid-row-gap: 20px;
		margin-left: auto;
		margin-right: auto;
		margin-top: 5%;
		text-align: center;
		width: 60%;
	}

</style>
