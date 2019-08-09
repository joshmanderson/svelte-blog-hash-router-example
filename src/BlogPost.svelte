<script>
  import Nav from "./Nav.svelte";
  import posts from "./posts.js";

  export let hash;

  $: postPromise = new Promise((resolve, reject) =>
    setTimeout(() => {
      const post = posts.find(post => `#post-${post.id}` === hash);

      if (post) {
        resolve(post);
      } else {
        reject(new Error("Couldn't find post!"));
      }
    }, 500)
  );
</script>

<Nav />

{#await postPromise}
  <p>Loading...</p>
{:then post}
  <h1>{post.title}</h1>
  <p>{post.content}</p>
{:catch error}
  <p>{error.message}</p>
{/await}
