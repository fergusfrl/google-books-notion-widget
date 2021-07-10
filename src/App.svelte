<script>
	export let bookTitle;
</script>

<main>
	<input bind:value={bookTitle} placeholder="Search book title">
</main>

<style>
	main {
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>