<script>
  export let size = 24;
</script>

<div class="loading">
  <div class="spinner" style="--size: {size}px" aria-label="Carregando"></div>
</div>

<style>
  .loading {
    display: flex;
    justify-content: center;
    width: 100%;
  }
  .spinner {
    width: var(--size);
    height: var(--size);
    border: 4px solid transparent;
    border-top-color: black;
    border-radius: 50%;
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    to {
      transform: rotate(360deg);
    }
  }
</style>
