<script>
  export let label = "";
  export let checked = false;
  export let onChange;
  export let error = "";
</script>

<div class="checkbox">
  <label class="checkbox-label">
    <input type="checkbox" bind:checked on:change={onChange} />
    <span class="checkmark"></span>
    {label}
  </label>
  {#if error}
    <span class="error">{error}</span>
  {/if}
</div>

<style>
  .checkbox {
    margin-bottom: 1rem;
  }

  .checkbox-label {
    display: flex;
    align-items: center;
    cursor: pointer;
    position: relative;
  }

  input[type="checkbox"] {
    display: none;
  }

  .checkmark {
    width: 20px;
    height: 20px;
    background-color: #2b2b2b;
    border-radius: 5px;
    border: 2px solid #aaa;
    margin-right: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition:
      background-color 0.2s,
      border-color 0.2s;
  }

  input[type="checkbox"]:checked + .checkmark {
    background-color: #3b3b3b;
    border-color: #fff;
  }

  .checkmark::after {
    content: "";
    display: none;
    width: 5px;
    height: 10px;
    border: solid white;
    border-width: 0 2px 2px 0;
    transform: rotate(45deg);
  }

  input[type="checkbox"]:checked + .checkmark::after {
    display: block;
  }

  .error {
    color: red;
    font-size: 0.875rem;
    margin-top: 5px;
  }
</style>
