<script context="module" lang="ts">
  export async function load(ctx) {
    let slug = ctx.page.params.slug;
    return {props: {slug}}
  }
</script>
<script lang="ts">
  import { gql } from '@apollo/client/core';
  import { query } from 'svelte-apollo';
  
  const post = query<any, any>(gql`
  query PostBy($slug: ID!) {
  post(id: $slug, idType: SLUG) {
      id
      title
      slug
      excerpt
      content
  }
}
`, {
  variables: {
    slug: "post-41"
  }
});
</script>

{#if $post.error}
<p>Error</p>
{/if}
{#if $post.loading}
<p>Loading</p>
{/if}

{#if $post.data}
<h1>{$post.data.post.title}</h1>
<article>
  {@html $post.data.post.content}
</article>
{/if}

