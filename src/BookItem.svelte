<script>
  export let title;
  export let subtitle;
  export let authors;

  const handleBookSelect = () => {
    fetch('https://us-central1-test-database-200da.cloudfunctions.net/createPage', {
      method: 'POST',
      body: JSON.stringify({
        title,
        author: authors.join(', '),
      }),
    });
  };
    
</script>

<div class="book-item" on:click={handleBookSelect}>
  <p>{title}</p>
  <p class="subtitle">{subtitle}</p>
  <p class="subtitle">{authors[0]}</p>
</div>

<style>
  .book-item {
    border: 1px grey solid;
    padding: 1em;
    margin: 1em;
    cursor: pointer;
  }

  .subtitle {
		color: grey;
		font-size: small;
	}
</style>
