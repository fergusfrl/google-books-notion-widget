<script>
import App from "./App.svelte";

  export let title;
  export let subtitle;
  export let authors;
  export let link;

  let adding = false;

  const handleBookSelect = () => {
    adding = true;
    fetch('https://us-central1-test-database-200da.cloudfunctions.net/createPage', {
      method: 'POST',
      body: JSON.stringify({
        title,
        author: authors.join(', '),
        subtitle,
        link
      }),
    }).finally(() => {
      adding = false;
    })
  };
    
</script>

<div class="book-item" on:click={handleBookSelect}>
  {#if adding}
    Adding {title}...
  {:else}
    <div class="book-title">
      <h4>{title}</h4>
      {#if subtitle}
        <p class="subtitle">{subtitle}</p>
      {/if}
    </div>
    {#if authors}
      <p class="subtitle">By {authors.join(', ')}</p>
    {/if}
  {/if} 
</div>

<style>
  .book-item {
    border: 1px #ccc solid;
    padding: 0.7em;
    margin: 1em 0;
    cursor: pointer;
    transition: 0.2s ease;
  }

  .book-item:hover {
    background-color: #ccc;
  }

  .book-title {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  h4 {
    padding: 0;
    margin: 0;
  }

  p {
    padding: 0;
    margin: 0;
  }
  .subtitle {
		color: grey;
		font-size: small;
	}
</style>
