<script context="module">
	export const prerender = true;
</script>

<script lang="ts">
	import { gql } from '@apollo/client/core/core.cjs.js';
	import { query } from 'svelte-apollo';

	const posts = query<any, any>(gql`
		{
			posts {
				nodes {
					id
					title
					slug
					excerpt
				}
			}
		}
	`);
</script>

<svelte:head>
	<title>Home</title>
</svelte:head>

<h1>Headless WordPress with Svelte and SvelteKit</h1>

{#if $posts.loading}
	<div>Loading</div>
{/if}

{#if $posts.error}
	<li>Error: {$posts.error.message}</li>
{/if}

{#if $posts.data}
	<ul>
		{#each $posts.data.posts.nodes as post}
			<li>
				<h2><a href={`/${post.slug}`}>{post.title}</a></h2>
				<p>{@html post.excerpt}</p>
			</li>
		{/each}
	</ul>
{/if}

<style>
	ul {
		padding: 0;
	}
	li {
		list-style: none;
	}
	a {
		text-decoration: none;
	}
</style>
