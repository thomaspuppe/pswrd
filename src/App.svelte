<script>
	import Router from 'svelte-spa-router'
	import {location, link } from 'svelte-spa-router'
	import active from 'svelte-spa-router/active'

	import Home from './modules/Home.svelte'
	import Horse from './modules/Horse.svelte'
	import Dice from './modules/Dice.svelte'
	import Classic from './modules/Classic.svelte'
	import Hash from './modules/Hash.svelte'
	import NotFound from './modules/NotFound.svelte'

	const routes = {
		// Exact path
		'/': Home,
		'/horse': Horse,
		'/dice': Dice,
		'/classic': Classic,
		'/hash': Hash,
		// Catch-all
		// This is optional, but if present it must be the last
		'*': NotFound,
	}

	export let name;
</script>

<main>

	<nav class="tabs">
		<a href="/horse" use:link use:active>🐴&emsp;Words</a>
		<a href="/dice" use:link use:active>🎲&emsp;Dice</a>
		
		<a href="/hash" use:link use:active>🎏&emsp;Hash</a>
		<a href="/classic" use:link use:active>🤬&emsp;Classic</a>
	</nav>

	<h1>Password Generator</h1>

	<Router {routes}/>

	<hr>
	{ name } | current location is: {$location}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 900px;
		margin: 0 auto;
	}
	/* TABS ******************************** */
	.tabs {
		padding: 30px;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		background-color: #f0f6f8;
	}
	.tabs a {
		cursor: pointer;
		color: #0e1635;
		border-radius: 5px;
		padding: 10px;
		text-align: center;
		width: 100%;
		margin-right: 5px;
		background-color: #f0f6f8;
		font-weight: 700;
		transition: box-shadow 0.3s;
	}
	/* Style for "active" links; need to mark this :global because the router adds the class directly */
	:global(.tabs a.active) {
		box-shadow: 2px 2px 5px 0px rgba(138, 133, 133, 0.75);
	}
</style>