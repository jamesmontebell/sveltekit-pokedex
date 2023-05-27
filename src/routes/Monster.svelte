<script lang="ts">
	import type { IndexMonster } from './+page';
	export let monster: IndexMonster;

	import { caughtMonsters } from '../lib/stores';

	const catchMonster = () => {
		caughtMonsters.update((monsters) => {
			return [...monsters, monster];
		});
		console.log('Catching monster', monster);
	};
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="monster">
	<div class="monster-content">
		<img src={monster.image} alt={monster.name} />
		<div class="name">{monster.name.charAt(0).toUpperCase() + monster.name.slice(1)}</div>
		<div on:click={catchMonster}>
			<button class="catch">Catch</button>
		</div>
	</div>
	<div class="monster-id">
		{monster.id}
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');

	* {
		font-family: lato, sans-serif;
	}

	.name {
		color: white;
	}

	.catch {
		background-color: #0c1815;
		border: 1px solid #aaa;
		border-radius: 10px;
		padding: 4px;
		color: white;
	}

	.monster-id {
		position: absolute;
		top: 8px;
		left: 8px;
		font-size: 0.8em;
		color: #aaa;
	}

	.monster {
		width: 200px;
		margin: 10px;
		padding: 10px;
		position: relative;
		background-color: #0c1815;
		border-radius: 20px;
		border: 1px solid #aaa;
	}

	.monster:hover {
		background-color: #ddd;
		transition: ease-in-out 0.2s;
	}

	.monster:hover .name {
		color: #0c1815;
		transition: ease-in-out 0.2s;
	}

	.monster-content {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>
