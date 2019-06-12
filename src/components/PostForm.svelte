<script>
  let title = "";
  let body = "";
  let loading = false;

  const apiBaseUrl =
    "https://ndb99xkpdk.execute-api.eu-west-2.amazonaws.com/dev";

  async function onSubmit(e) {
    e.preventDefault();
    if (title.trim() === "" || body.trim() === "") {
      return;
    }

    loading = true;

    const newPost = { title, body };
    const res = await fetch(`${apiBaseUrl}/post`, {
      method: "POST",
      body: JSON.stringify(newPost)
    });
    const post = await res.json();

    title = "";
    body = "";
    loading = false;
  }
</script>

<style>
  .form-container {
    margin: 50px 0;
  }
</style>

<div class="form-container">
  {#if !loading}
    <form on:submit={onSubmit}>
      <div class="input-field">
        <label for="title">Title</label>
        <input type="text" id="title" bind:value={title} />
      </div>
      <div class="input-field">
        <label for="body">Body</label>
        <input type="text" id="body" bind:value={body} />
      </div>
      <button type="submit" class="waves-effect waves-light btn">Submit</button>
    </form>
  {:else}
    <div class="preloader-wrapper small active">
      <div class="spinner-layer spinner-green-only">
        <div class="circle-clipper left">
          <div class="circle" />
        </div>
        <div class="gap-patch">
          <div class="circle" />
        </div>
        <div class="circle-clipper right">
          <div class="circle" />
        </div>
      </div>
    </div>
  {/if}
</div>
