<script>
  import { onMount } from "svelte";

  export let routes;

  let currentRoute;
  let hash;

  $: indexRoute = routes.find(route => route.isIndexRoute);
  $: notFoundRoute = routes.find(route => route.isNotFoundRoute);

  $: {
    if (!hash || !hash.substring(1)) {
      currentRoute = indexRoute;
    } else {
      const matchedRoute = routes.find(route =>
        route.usesPartialHash
          ? hash.substring(1).startsWith(route.hash)
          : route.hash === hash.substring(1)
      );

      currentRoute = matchedRoute || notFoundRoute || indexRoute;
    }
  }

  function updateHash() {
    hash = window.location.hash;
  }

  onMount(() => {
    updateHash();

    window.addEventListener("hashchange", updateHash, false);

    return () => window.removeEventListener("hashchange", updateHash);
  });
</script>

{#if currentRoute}
  <svelte:component this={currentRoute.component} {hash} />
{/if}
