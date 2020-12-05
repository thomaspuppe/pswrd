<script>
    let number = Math.floor(Math.random() * 6 + 1)

	function handleClick() {
		number = Math.floor(Math.random() * 6 + 1)
	}
</script>
<p>{number}</p>

<!-- TODO: das zentral reingeben, oder in App.svelte haben, oder als Subcomponent laden? -->
<button on:click={handleClick}>🔁&emsp;new password</button>