<script lang="ts">
	import { page } from '$app/stores';
	import { caughtMonsters } from '../lib/stores';
</script>

<div class="navbar">
	<a class:active={$page.url.pathname == '/'} href="/">Home</a>
	<a class:active={$page.url.pathname == '/my-monsters'} href="/my-monsters"
		>My Pokemon ({$caughtMonsters.length})
	</a>
</div>

<div class="container">
	<slot />
</div>

<style>
	* {
		font-family: lato, sans-serif;
	}
	.navbar {
		display: flex;
		justify-content: space-between;
		background-color: antiquewhite;
		padding: 10px;
		border: 1px solid #aaa;
		margin: 6px;
		margin-left: 100px;
		margin-right: 100px;
		margin-top: 50px;
	}
	.navbar a {
		color: black;
		text-decoration: none;
		cursor: pointer;
	}
	.navbar a.active {
		border: 1px solid #aaa;
		border-radius: 4px;
	}
	.navbar a:hover {
		color: rgba(0, 0, 0, 0.568);
	}
	:global(body) {
		margin: 0;
	}
	.container {
		max-width: 90%;
		margin: auto;
		width: 1200px;
	}
</style>
