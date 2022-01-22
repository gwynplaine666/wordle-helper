<script>
	import alphabet from '$lib/alphabet.js';
	import { createEventDispatcher } from 'svelte';

	export let title;
	export let isCorrectWord = false;
	export let selectedWords;
	export let selectedOtherWords;
	const dispatch = createEventDispatcher();
	const onClick = (event) => dispatch('wordSelect', event.target.value);

	$: selectedWordsArr = alphabet.RU.map(i => {

		if (selectedOtherWords.includes(i)) {
			return {word: i, selected: false, disabled: true}
		}

		if (selectedWords.includes(i)) {
			return { word: i, selected: true };
		}
		return { word: i, selected: false };
	});

</script>
<div class='container'>
	<h3>{title}</h3>
	<div class='alphabet'>
		{#each selectedWordsArr as { word, selected, disabled }}
			<button disabled={disabled} class:correct-word={selected && isCorrectWord} class:wrong-word={selected && !isCorrectWord}
							class='button-24' on:click={onClick} value={word}>{word}</button>
		{/each}
	</div>
</div>


<style>
    h3 {
        margin: 0;
        text-align: center;
        padding-bottom: 5px;
        color: white;
    }

    .alphabet {
        border: 2px solid #dc3372;
        display: grid;
        grid-template-columns: repeat(5, 15%);
        grid-column-gap: 20px;
        justify-content: center;
        grid-row-gap: 10px;
        padding: 10px;
        width: auto;
    }

    button {
        border: none;
        background-color: white;
        font-family: inherit;
        padding: 10px;
        cursor: pointer;
    }

    .button-24 {
        background: #decaca;
        border: 1px solid #FF4742;
        border-radius: 6px;
        box-shadow: rgba(0, 0, 0, 0.1) 1px 2px 4px;
        box-sizing: border-box;
        color: black;
        cursor: pointer;
        display: inline-block;
        font-family: nunito, roboto, proxima-nova, "proxima nova", sans-serif;
        font-size: 16px;
        font-weight: 800;
        line-height: 16px;
        min-height: 40px;
        outline: 0;
        padding: 12px 14px;
        text-align: center;
        text-rendering: geometricprecision;
        text-transform: none;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
        vertical-align: middle;
        transition: 0.3s;
    }

    .button-24:hover,
    .button-24:active {
        background-color: initial;
        background-position: 0 0;
        color: #FF4742;
    }

    .button-24:active {
        opacity: .5;
    }

    .button-24.correct-word:hover {
        color: white;
    }

    .button-24.correct-word {
        background: green;
        border: 1px solid green;
    }

		.button-24.wrong-word {
        background: red;
        border: 1px solid red;
		}
		.button-24:disabled {
				background: gray;
        border: 1px solid gray;
    }
</style>