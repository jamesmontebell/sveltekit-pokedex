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
	<div on:click={catchMonster}>
		<div class="monster-content">
			<img src={monster.image} alt={monster.name} />
			{monster.name.charAt(0).toUpperCase() + monster.name.slice(1)}
		</div>
		<div class="monster-id">
			{monster.id}
		</div>
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');

	* {
		font-family: lato, sans-serif;
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
		background-color: #eee;
	}

	.monster:hover {
		background-color: #ddd;
		transition: ease-in-out 0.2s;
	}

	.monster-content {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>
