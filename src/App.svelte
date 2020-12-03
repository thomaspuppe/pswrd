<script>
	export let name;
</script>

<main>

	<ul class="tabs">
		<li class="active">🐴 Words</li>
		<li>🎲 Dice</li>
		<li>Easy</li>
		<li>Hard</li>
	</ul>

	<h1>Password Generator</h1>
	<p>Easy password generation for {{ name }}</p>
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
		list-style: none;
	}
	.tabs li {
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
	.tabs li.active {
		box-shadow: 2px 2px 5px 0px rgba(138, 133, 133, 0.75);
	}
</style>