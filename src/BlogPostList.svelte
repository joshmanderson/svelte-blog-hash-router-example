<script>
  import Nav from "./Nav.svelte";
  import posts from "./posts.js";

  let postsPromise = new Promise(resolve =>
    setTimeout(() => resolve(posts), 500)
  );
</script>

<Nav />

{#await postsPromise}
  <p>Loading...</p>
{:then posts}
  <ul>
    {#each posts as post}
      <li>
        <a href={`#post-${post.id}`}>{post.title}</a>
      </li>
    {/each}
  </ul>
{/await}
