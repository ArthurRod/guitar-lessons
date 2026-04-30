<script>
  import Fuse from "fuse.js";
  import {onMount} from "svelte";
  import Loading from "./Loading.svelte";

  export let posts = [];

  let query = "";
  let results = [];
  let fuse;
  let loading = true;

  const formatDate = (dateStr) =>
    new Date(dateStr).toLocaleDateString("pt-BR", {
      year: "numeric",
      month: "short",
      day: "numeric",
    });

  onMount(() => {
    const params = new URLSearchParams(window.location.search);
    query = params.get("q")?.trim() || "";

    if (posts.length > 0) {
      fuse = new Fuse(posts, {
        keys: ["data.title", "data.description", "data.author", "data.tags"],
        minMatchCharLength: 2,
        includeMatches: true,
        threshold: 0.3,
      });
      updateResults();
    } else {
      loading = false;
    }
  });

  $: if (fuse && query !== undefined) {
    updateResults();
  }

  function updateResults() {
    results = query.length > 0 ? fuse.search(query).map((r) => r.item) : posts;
    loading = false;
  }
</script>

<section id="search-posts">
  {#if loading}
    <Loading />
  {:else if results.length > 0}
    <ul>
      {#each results as post}
        <li>
          <a href={`/posts/${post.id}`}>
            <img
              width={720}
              height={360}
              src={post.data.heroImage}
              alt={post.data.title}
            />
            <h4 class="title">{post.data.title}</h4>
            <p class="date">{formatDate(post.data.pubDate)}</p>
          </a>
        </li>
      {/each}
    </ul>
  {:else}
    <p>Nenhum post encontrado.</p>
  {/if}
</section>
