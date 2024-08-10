<script>
	import { spring } from 'svelte/motion';
	import { goto } from '$app/navigation';
	import { rightQuest } from '../../stores';
	import { wrongQuest } from '../../stores';
	
	/**
     * @type {number | undefined}
     */
	let intervalId;
	let tau = 3000;
	let rightCount = 0;
	let wrongCount = 0;
	
	const displayed_count_right = spring();
	$: displayed_count_right.set(rightCount);
	$: offset_right = modulo($displayed_count_right, 1);

	const displayed_count_wrong = spring();
	$: displayed_count_wrong.set(wrongCount);
	$: offset_wrong = modulo($displayed_count_wrong, 1);

	/**
	 * @param {number} n
	 * @param {number} m
	 */
	function modulo(n, m) {
		// handle negative numbers
		return ((n % m) + m) % m;
	}

	function contar() {
		if (rightCount < $rightQuest) {
			rightCount += 1;
		}

		if (wrongCount < $wrongQuest) {
			wrongCount += 1;
		}

		if (rightCount == $rightQuest && wrongCount == $wrongQuest) {
			clearInterval(intervalId);
		}
	}

	intervalId = setInterval(contar, 20);

	
</script>

<div class="flex-container">
	<div class="counter-viewport-right">
		<div class="counter-digits" style="transform: translate(0, {100 * offset_right}%)">
			<strong class="hidden" aria-hidden="true">{Math.floor($displayed_count_right + 1)}</strong>
			<strong>{Math.floor($displayed_count_right)}</strong>
		</div>
		
	</div>
	
	<div class="counter-viewport-wrong">
		<div class="counter-digits" style="transform: translate(0, {100 * offset_wrong}%)">
			<strong class="hidden" aria-hidden="true">{Math.floor($displayed_count_wrong + 1)}</strong>
			<strong>{Math.floor($displayed_count_wrong)}</strong>
			
		</div>
	</div>
</div>

<div class="flex-container">
	<h1 id="resp_corr">Respuestas correctas</h1>
	<h1 id="resp_incorr">Incorrectas</h1>
</div>

<div id="button-container">
	<button on:click={() => goto('/quiz')}>Volver a intentar</button>
</div>


<style>
	.flex-container {
		display: flex;
	}

	.counter-viewport-right {
		position: relative;
		width: 30em;
		height: 15em;
		margin-top: 5em;
		overflow: hidden;
		text-align: center;
	}

	.counter-viewport-right strong {
		position: absolute;
		display: flex;
		width: 100%;
		height: 100%;
		font-weight: 400;
		color: #a8e6cf;
		font-size: 15rem;
		align-items: center;
		justify-content: center;
	}

	.counter-viewport-wrong {
		position: relative;
		width: 30em;
		height: 15em;
		margin-top: 5em;
		overflow: hidden;
		text-align: center;
	}

	.counter-viewport-wrong strong {
		position: absolute;
		display: flex;
		width: 100%;
		height: 100%;
		font-weight: 400;
		color: #ff8b8b;
		font-size: 15rem;
		align-items: center;
		justify-content: center;
	}

	.counter-digits {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.hidden {
		top: -100%;
		user-select: none;
	}

	#resp_corr {
		color: #a8e6cf;
		margin-left: 1.5em;
	}

	#resp_incorr {
		color: #ff8b8b;
		margin-left: 5em;
	}
	
	button {
		width: 30rem;
		height: 7rem;
		cursor: pointer;
		transition: transform 0.3s ease-in-out;
		border: none;
		outline: none;
		font-size: 3rem;
		border-radius: 2rem;
		background-color: #91e7c7;
    }

	button:hover {
        background-color: var(--secondary-color);
        cursor: pointer;
        transform: scale(1.1);
    }

	#button-container {
		text-align: center;
	}

</style>
