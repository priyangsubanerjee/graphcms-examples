<script context="module">
  import { GraphQLClient } from 'graphql-request';
  export async function load() {
    const graphcms = new GraphQLClient(
      'https://api-eu-central-1.graphcms.com/v2/ck8sn5tnf01gc01z89dbc7s0o/master',
      {
        headers: {},
      }
    )
    const { products } = await graphcms.request(
      `query Products { 
        products {
          slug
          name
        }
      }`
    )
    return {
      props: {
        products,
      },
    }
  }
</script>

<script>
  export let products
</script>

<svelte:head>
  <title>SvelteKit project template</title>
</svelte:head>

<h1>GraphCMS with SvelteKit and GraphQL Request</h1>

{#each products as product}
  <p>
    <a href="/product/{product.slug}">
      {product.name}
    </a>
  </p>
{/each}
