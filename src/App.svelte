<script>
import BookItem from "./BookItem.svelte";

	const searchBooks = async () => {
		return await fetch(`https://www.googleapis.com/books/v1/volumes?q=${searchTerm}&maxResults=5`)
			.then(res => res.json());
	}

	let searchTerm = 'this is going to hurt';
	let books = searchBooks();

	const handleSearch = (e) => {
		e.preventDefault();
		books = searchBooks();
	};
</script>

<main>
	<form>
		<input bind:value={searchTerm} placeholder="Search by title or author">
		<button on:click={handleSearch} type="submit">Search</button>
	</form>

	{#await books}
		<p>searching...</p>
	{:then bookList}
		{#if bookList && bookList.items}
			{#each bookList.items as { selfLink, volumeInfo: { title, subtitle, authors } }}
				<BookItem title={title} subtitle={subtitle} authors={authors} link={selfLink} />
			{/each}
		{/if}
	{/await}	
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