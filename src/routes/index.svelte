<script lang="ts">
  import { gql } from '@apollo/client/core';
  import { query } from 'svelte-apollo';
  
  const posts = query<any, any>(gql`{
  posts {
    nodes {
      id
      title
      slug
      excerpt
    }
  }
}`);
</script>

<h1>Headless WordPress with Svelte and SvelteKit</h1>

<ul>
  {#if $posts.loading}
  <li>Loading</li>
  {:else if $posts.error}
  <li>Error: {$posts.error.message}</li>
  {:else}
    {#each $posts.data.posts.nodes as post}
      <li><h2><a href={`/${post.slug}`}>{post.title}</a></h2><p>{@html post.excerpt}</p></li>
    {/each}
  {/if}
</ul>