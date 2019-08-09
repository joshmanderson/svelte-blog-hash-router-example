<script>
  import HashRouter from "./HashRouter.svelte";
  import Home from "./Home.svelte";
  import NotFound from "./NotFound.svelte";
  import About from "./About.svelte";
  import BlogPost from "./BlogPost.svelte";
  import BlogPostList from "./BlogPostList.svelte";

  const routes = [
    { hash: "home", isIndexRoute: true, component: Home },
    { hash: "not-found", isNotFoundRoute: true, component: NotFound },
    { hash: "about", component: About },
    { hash: "posts", component: BlogPostList },
    { hash: "post-", usesPartialHash: true, component: BlogPost },
  ];
</script>

<HashRouter {routes} />
