<script>
	let fields = new Array(9).fill(null);
	let result = null;
	let player = 'X';
	const checkCombos = [
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8],
		[2, 4, 6]
	];
	function setField(i) {
		fields[i] = player;
		fields = [...fields];
		player = player === 'X' ? 'O' : 'X';

		if (!fields.includes(null)) {
			result = 'Draw';
		} else {
			isWinner();
		}
	}

	function isWinner() {
		for (let i = 0; i < checkCombos.length; i++) {
			if (fields[checkCombos[i][0]] != null) {
				if (
					fields[checkCombos[i][0]] == fields[checkCombos[i][1]] &&
					fields[checkCombos[i][1]] == fields[checkCombos[i][2]]
				) {
					result = fields[checkCombos[i][0]] + ' is Winner';
				}
			}
		}
	}

	function restart() {
		fields = new Array(9).fill(null);
		result = null;
		player = 'X';
	}
</script>

<main class="pt-20 text-center h-screen bg-[#001219] text-[#fdf0d5] flex flex-col items-center">
	<h1 class="mb-5 text-5xl font-bold">TIC TAC TOE</h1>

	{#if !result}
		<h3 class="text-lg">{player}'s turn</h3>
		<div class="w-60 h-60 flex flex-wrap">
			{#each fields as field, i}
				<button
					class="w-20 h-20 cursor-pointer hover:bg-[#86c2da1c] border-solid border-2 border-[#fdf0d5] m-0"
					on:click|once={() => {
						setField(i);
					}}>{field ? field : ''}</button
				>
			{/each}
		</div>
	{:else}
		<div>{result}</div>
		<button on:click={restart} class="border-[#fdf0d5] border-solid border-2 p-3">restart</button>
	{/if}
</main>
