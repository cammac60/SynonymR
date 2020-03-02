<script>

	document.title = 'SynonymR';

	let errorMsg;
	let curWord;
	let foundWords = [];
	let loading = false;

	const fetchSyns = async () => {
		const url = `https://www.dictionaryapi.com/api/v3/references/thesaurus/json/${curWord}?key=3d79f969-d355-4060-9017-28021b58745e`;
		const response = await fetch(url);
		if (!response.ok) {
			throw new Error('Error: The synonyms couldn\'t be found.')
		}
		const data = await response.json();
		return data;
	};

	const handleSubmit = () => {
		if (validateSubmit()) {
			errorMsg = validateSubmit();
		} else {
				errorMsg = '';
				grabSyns();
		}
	};

	const validateSubmit = () => {
		if (!curWord) {
			return 'Please enter a word.';
		} else {
				return false;
		}
	};

	const grabSyns = async () => {
		loading = true;
		try {
			const response = await fetchSyns();
			const items = response[0].meta.syns[0];
			foundWords = items;
			loading = false;
			console.log(foundWords);
		} catch(error) {
				errorMsg = 'There was a problem getting your synonyms. Please try again.'
				console.log(error);
		}
	};

</script>

<main>

	<h1>SynonymR</h1>
	<div class="form">
		<input type="text" placeholder="Enter a word" bind:value={curWord}/>
		<button on:click={handleSubmit} disabled={loading}>Find Synonyms</button>
	</div>
	<p class="error">{errorMsg || ''}</p>
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
