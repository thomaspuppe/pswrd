<script>
    let number = Math.floor(Math.random() * 6 + 1)

	function handleClick() {
		number = Math.floor(Math.random() * 6 + 1)
	}
</script>
<p>{number}</p>
<button on:click={handleClick}>again</button>