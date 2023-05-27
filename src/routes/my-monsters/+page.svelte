<script lang="ts">
	import { caughtMonsters } from '../../lib/stores';
	import Monster from '../Monster.svelte';
</script>

<h1>My Pokemon</h1>
<div class="monsters">
	{#each $caughtMonsters as monster}
		<Monster {monster} />
	{/each}
</div>

<style>
	.monsters {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
	}

	h1 {
		text-align: center;
		color: white;
	}
</style>
