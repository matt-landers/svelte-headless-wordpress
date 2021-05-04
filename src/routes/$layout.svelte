<script lang="ts">
  import { ApolloClient, InMemoryCache } from '@apollo/client/core';
  import { setClient } from 'svelte-apollo';
  
  const client = new ApolloClient({
    uri: 'https://headlessfw.wpengine.com/graphql',
    cache: new InMemoryCache()
  });
  setClient(client);
</script>

<slot></slot>