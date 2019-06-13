<script>
  import { onMount } from "svelte";
  import PostForm from "../components/PostForm.svelte";

  const apiBaseUrl =
    "https://ndb99xkpdk.execute-api.eu-west-2.amazonaws.com/dev";

  let posts = [];
  let editingPost = {
    body: "",
    title: "",
    id: null
  };

  onMount(async () => {
    const res = await fetch(`${apiBaseUrl}/posts`);
    posts = await res.json();
  });

  function postCreated(e) {
    e.preventDefault();
    if (posts.find(p => p.id === e.detail.id)) {
      const index = posts.findIndex(p => p.id === e.detail.id);
      let postsUpdated = posts;
      postsUpdated.splice(index, 1, e.detail);
      posts = postsUpdated;
    } else {
      posts = [e.detail, ...posts];
    }

    editingPost = {
      body: "",
      title: "",
      id: null
    };
  }

  function editPost(post) {
    editingPost = post;
  }

  function deletePost(id) {
    fetch(`${apiBaseUrl}/post/${id}`, {
      method: "DELETE"
    })
      .then(res => res.json())
      .then(() => (posts = posts.filter(p => p.id !== id)));
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
  <div class="col s6">
    <PostForm on:postCreated={postCreated} {editingPost} />
  </div>
</div>
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
