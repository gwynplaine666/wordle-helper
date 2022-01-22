<script>
	import Alphabet from '../components/Alphabet.svelte';
	import alphabet from '$lib/alphabet.js';
 	let selectedRightWords = [];
	let selectedWrongWords = [];

	const addWordToRight = (event) => {
		if (selectedRightWords.includes(event.detail)) {
			selectedRightWords = selectedRightWords.filter(i => i !== event.detail)
			return;
		}
		selectedRightWords = [...selectedRightWords, event.detail]
	}
	const addWordToWrong = (event) => {
		if (selectedWrongWords.includes(event.detail)) {
			selectedWrongWords = selectedWrongWords.filter(i => i !== event.detail)
			return;
		}
		selectedWrongWords = [...selectedWrongWords, event.detail]
	}

	$: otherWords = alphabet.RU.filter(i => !selectedRightWords.includes(i)).filter(i => !selectedWrongWords.includes(i))
</script>

<div class='Container'>
<div class='Words-buttons'>
	<Alphabet title='ЕСТЬ В СЛОВЕ' on:wordSelect={addWordToRight} selectedOtherWords={selectedWrongWords} selectedWords={selectedRightWords} isCorrectWord/>
	<Alphabet title='НЕТ В СЛОВЕ' on:wordSelect={addWordToWrong}  selectedOtherWords={selectedRightWords} selectedWords={selectedWrongWords}/>
</div>
<div class='Result'>
	<div>
		В слове точно есть буквы:
		<span class='green-word'>{selectedRightWords.join(", ")}</span>
	</div>
	<div>
		В слове точно нет букв:
		<span class='red-word'>{selectedWrongWords.join(", ")}</span>
	</div>
	<div>
		{#if otherWords.length}Неизвестные буквы:<span class='unknown-word'>{otherWords.join(", ")}</span>{/if}
	</div>
</div>
</div>
<style>
		.Container {
				padding: 10px 30px;
				/*display: grid;*/
				/*justify-content: center;*/
		}
	.Words-buttons {
      padding: 20px 20px 0;
			font-family: Comic Sans MS,serif;
			display: grid;
			grid-template-columns: 33% 33%;
			grid-column-gap: 20%;
			justify-content: space-between;
  }
	.Result {
      padding: 20px 20px 0;
      font-family: Comic Sans MS,serif;
			color: white;
			font-size: 1.3em;
	}
	.green-word {
			color: greenyellow;
	}
	.red-word {
			color: red;
	}
	.unknown-word {
			padding-left: 5px;
	}
</style>