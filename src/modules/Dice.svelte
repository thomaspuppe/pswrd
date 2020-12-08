<script>
	import PasswordStage from './blocks/PasswordStage.svelte'

    let number = Math.floor(Math.random() * 6 + 1)

	function handleClick() {
		number = Math.floor(Math.random() * 6 + 1)
	}
</script>

<PasswordStage password={ number } />

<!-- TODO: das zentral reingeben, oder in App.svelte haben, oder als Subcomponent laden? -->
<button on:click={handleClick}>🔁&emsp;new password</button>