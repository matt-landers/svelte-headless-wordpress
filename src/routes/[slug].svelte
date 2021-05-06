<script context="module" lang="ts">
	import { browser } from '$app/env';
	export const router = browser;

	export async function load(ctx) {
		let slug = ctx.page.params.slug;
		return { props: { slug } };
	}
</script>

<script lang="ts">
	export let slug;
	import { gql } from '@apollo/client/core/core.cjs.js';
	import { query } from 'svelte-apollo';

	const post = query<any, any>(
		gql`
			query PostBy($slug: ID!) {
				post(id: $slug, idType: SLUG) {
					id
					title
					slug
					excerpt
					content
				}
			}
		`,
		{
			variables: {
				slug
			}
		}
	);
</script>

<svelte:head>
	{#if $post.data}
		<title>{$post.data.post.title}</title>
	{/if}
</svelte:head>

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
