<script>
  import { Link } from "svelte-routing";
</script>

<nav>
  <div class="nav-wrapper">
    <div class="container">
      <Link to="/" class="brand-logo">Svelte Tutorial</Link>
      <ul id="nav-mobile" class="right">
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
      </ul>
    </div>

  </div>
</nav>
