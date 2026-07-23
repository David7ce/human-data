<script>
  export let src;
  export let alt = "";
</script>

<style>
  .avatar {
    width: 130px;
    height: 130px;
    margin: 0 auto;
    border-radius: 50%;
    border: 3px solid #ff00ff;
    background-size: cover;
    background-position: center;
    box-shadow: 0 0 20px #ff00ff;
  }
</style>

<div
  class="avatar"
  role="img"
  aria-label={alt}
  style="background-image: url('{src}')"
></div>
