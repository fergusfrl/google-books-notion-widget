<script>
import BookItem from "./BookItem.svelte";

	let searchTerm;
	let books;

	const handleSearch = () => {
		books = searchBooks();
	}

	const searchBooks = async () => {
		return await fetch(`https://www.googleapis.com/books/v1/volumes?q=${searchTerm}&maxResults=5`)
			.then(res => res.json());
	}
</script>

<main>
	<input bind:value={searchTerm} placeholder="Search by title or author">
	<button on:click={handleSearch}>Search</button>

	{#await books}
		<p>searching...</p>
	{:then bookList}
		{#if bookList && bookList.items}
			{#each bookList.items as { volumeInfo: { title, subtitle, authors } }}
				<BookItem title={title} subtitle={subtitle} authors={authors} />
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