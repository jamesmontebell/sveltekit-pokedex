<script lang="ts">
	import { server_loads } from './../../.svelte-kit/generated/client/app.js';
	import type { PageData } from './$types';
	import type { IndexMonster } from './+page';
	import { page } from '$app/stores';
	import { generations } from './generations';
	import { goto } from '$app/navigation';
	import Monster from './Monster.svelte';
	import { slide } from 'svelte/transition';

	export let data: PageData;

	let form = {
		searchString: ''
	};
	let searchString = '';

	$: selectedMonsters = data.monsters.filter((monster) => {
		return monster.name.toLowerCase().includes(searchString.toLowerCase());
	});

	$: selectedGenerationId = $page.url.searchParams.get('generation_id') || '';

	const updateSearchParams = (key: string, value: string) => {
		const params = new URLSearchParams($page.url.search);
		params.set(key, value);
		goto(`?${params.toString()}`);
	};

	const submitSearch = (e: Event) => {
		searchString = form.searchString;
	};
</script>

<div class="generations">
	<button
		class="generation"
		class:active={selectedGenerationId == 'all'}
		on:click={() => updateSearchParams('generation_id', 'all')}>All</button
	>
	{#each generations as generation (generation.id)}
		<button
			class="generation"
			class:active={selectedGenerationId === generation.id.toString()}
			on:click={() => updateSearchParams('generation_id', generation.id.toString())}
		>
			{generation.main_region}
		</button>
	{/each}
</div>

<form class="search-form" on:submit|preventDefault={submitSearch}>
	<input
		class="search-field"
		type="text"
		bind:value={form.searchString}
		placeholder="Search Pokemon"
	/>
	<input class="" type="submit" value="Search" />
</form>

<div class="monsters">
	{#each selectedMonsters as monster (monster.id)}
		<Monster {monster} />
	{/each}
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');

	* {
		font-family: lato, sans-serif;
	}

	.generations {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
	}

	.generation {
		margin: 6px;
		padding: 5px 10px;
		border: 1px solid #aaa;
		background-color: #4685ff;
		cursor: pointer;
		border-radius: 10px;
	}

	.generation.active {
		background-color: #eee;
	}

	.generation:hover {
		background-color: #eee;
		transition: ease-in-out 0.3s;
	}

	.monsters {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
	}

	.search-form input[type='text'] {
		padding: 5px 10px;
		border-radius: 5px;
		width: 200px;
		height: 25px;
		border: 1px solid #aaa;
		border-radius: 10px;
	}

	.search-form {
		display: flex;
		justify-content: center;
		margin: 10px;
		align-items: center;
	}

	.search-form input[type='submit'] {
		padding: 5px 10px;
		border-radius: 5px;
		border: 1px solid #aaa;
		background-color: #4685ff;
		margin: 10px;
		border-radius: 10px;
	}
</style>
