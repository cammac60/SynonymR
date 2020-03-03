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
		} catch(error) {
				foundWords = [];
				loading = false;
				errorMsg = 'There was a problem getting your synonyms. Please try again.';
				console.log(error);
		}
	};

	const handleClick = ({ target }) => {
		const { id } = target;
		curWord = id;
		grabSyns();
	};

	const handleChange = () => {
		console.log('change');
		errorMsg = '';
	};

</script>

<main>

	<h1>SynonymR</h1>
	<div class="form">
		<input type="text" placeholder="Enter a word" bind:value={curWord} on:change={handleChange}/>
		<button on:click={handleSubmit} disabled={loading}>Find Synonyms</button>
	</div>
	<p class="error">{errorMsg || ''}</p>
	{#if loading}
		<div class="lds-roller">
			<div></div>
			<div></div>
			<div></div>
			<div></div>
			<div></div>
			<div></div>
			<div></div>
			<div></div>
		</div>
	{:else}
		<div class="word-wrapper">
			{#each foundWords as word}
				<p id={word} class="word" on:click={e => handleClick(e)}>{word}</p>
			{/each}
		</div>
	{/if}
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

	.word {
		cursor: pointer;
		user-select: none;
		-moz-user-select: none;
	}

	.word:hover {
		text-decoration: underline;
	}

	.word:active {
		color: #7CFCFC;
	}

	.lds-roller {
  display: inline-block;
  position: relative;
	margin-top: 20%;
  width: 80px;
  height: 80px;
	}

	.lds-roller div {
	  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
	  transform-origin: 40px 40px;
	}

	.lds-roller div:after {
	  content: " ";
	  display: block;
	  position: absolute;
	  width: 7px;
	  height: 7px;
	  border-radius: 50%;
	  background: #fff;
	  margin: -4px 0 0 -4px;
	}

	.lds-roller div:nth-child(1) {
	  animation-delay: -0.036s;
	}

	.lds-roller div:nth-child(1):after {
	  top: 63px;
	  left: 63px;
	}

	.lds-roller div:nth-child(2) {
	  animation-delay: -0.072s;
	}

	.lds-roller div:nth-child(2):after {
	  top: 68px;
	  left: 56px;
	}

	.lds-roller div:nth-child(3) {
	  animation-delay: -0.108s;
	}

	.lds-roller div:nth-child(3):after {
	  top: 71px;
	  left: 48px;
	}

	.lds-roller div:nth-child(4) {
	  animation-delay: -0.144s;
	}

	.lds-roller div:nth-child(4):after {
	  top: 72px;
	  left: 40px;
	}

	.lds-roller div:nth-child(5) {
	  animation-delay: -0.18s;
	}

	.lds-roller div:nth-child(5):after {
	  top: 71px;
	  left: 32px;
	}

	.lds-roller div:nth-child(6) {
	  animation-delay: -0.216s;
	}

	.lds-roller div:nth-child(6):after {
	  top: 68px;
	  left: 24px;
	}

	.lds-roller div:nth-child(7) {
	  animation-delay: -0.252s;
	}

	.lds-roller div:nth-child(7):after {
	  top: 63px;
	  left: 17px;
	}

	.lds-roller div:nth-child(8) {
	  animation-delay: -0.288s;
	}

	.lds-roller div:nth-child(8):after {
	  top: 56px;
	  left: 12px;
	}

	@keyframes lds-roller {
	  0% {
	    transform: rotate(0deg);
	  }
	  100% {
	    transform: rotate(360deg);
	  }
	}

</style>
