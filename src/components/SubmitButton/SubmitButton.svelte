<script>
  export let label = 'Submit';
  export let color = 'blue';
  export let onClick;
  
</script>

<button on:click={onClick} style="background-color: {color}; color: white;">
  {label}
</button>

<style>
  button {
    padding: 0.75rem 1.5rem;
    font-size: 1rem;
    border: none;
    cursor: pointer;
    border-radius: 5px;
  }

  button:hover {
    opacity: 0.9;
  }
</style>
