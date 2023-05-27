<script lang="ts">
	import { caughtMonsters } from '../../lib/stores';
	import Monster from '../Monster.svelte';
</script>

<h1>My monsters</h1>
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
</style>
