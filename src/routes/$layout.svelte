<script lang="ts">
	import { ApolloClient, InMemoryCache } from '@apollo/client/core/core.cjs.js';
	import { setClient } from 'svelte-apollo';

	const client = new ApolloClient({
		uri: 'https://headlesswpe.wpengine.com/graphql',
		cache: new InMemoryCache()
	});
	setClient(client);
</script>

<main>
	<slot />
</main>

<style>
	main {
		max-width: 680px;
		margin: 0 auto;
		font-family: sans-serif;
	}
	:global(body) {
		font-family: Montserrat, sans-serif;
		background: rgb(40, 44, 53);
		color: rgba(255, 255, 255, 0.88);
	}
	:global(a) {
		color: #0091ea;
		text-decoration: none;
	}
</style>
