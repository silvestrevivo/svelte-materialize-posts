<script>
  import { onMount } from "svelte";

  const apiBaseUrl =
    "https://ndb99xkpdk.execute-api.eu-west-2.amazonaws.com/dev";

  let posts = [];

  onMount(async () => {
    const res = await fetch(`${apiBaseUrl}/posts`);
    posts = await res.json();
  });

  function editPost(post) {
    console.log("post", post);
  }

  function deletePost(post) {
    console.log("post", post);
  }
</script>

<style>
  .card .card-content .card-title {
    margin-bottom: 0;
  }

  .card .card-content p.timestamp {
    color: #999;
    margin-bottom: 15px;
  }
</style>

<div class="row">
  {#each posts as post}
    <div class="col s6">
      <div class="card">
        <div class="card-content">
          <p class="card-title">{post.title}</p>
          <p class="timestamp">{post.createdAt}</p>
          <p>{post.body}</p>
        </div>
        <div class="card-action">
          <button class="btn" on:click={() => editPost(post)}>Edit</button>
          <button class="btn" on:click={() => deletePost(post.id)}>
            Delete
          </button>
        </div>
      </div>
    </div>
  {:else}
    <h3>Loading posts...</h3>
    <div class="progress">
      <div class="indeterminate" />
    </div>
  {/each}
</div>
