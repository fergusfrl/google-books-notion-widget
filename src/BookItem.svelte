<script>
  import { Client } from "@notionhq/client";

  export let title;
  export let subtitle;
  export let authors;

  const notion = new Client({ auth: __myapp.env.NOTION_API_KEY });
  const databaseId = __myapp.env.NOTION_DATABASE_ID;

  const handleBookSelect = () => {
    notion.request({
      path: 'pages',
      method: 'post',
      body: { 
        parent: { database_id: databaseId },
        properties: {
          Name: {
            title: [ { text: { content: title } } ]
          } ,
          Author: {
            rich_text: [ { text: { content: authors.join(', ') } } ]
          },
          Status: {
            select: { name: 'To Order' }
          }
        }
       }
    });
  }
    
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
