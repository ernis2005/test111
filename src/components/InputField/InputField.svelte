<script>
  export let label = "";
  export let required = false;
  export let inputValue = "";
  export let maxLength = 17; 
  export let type = "text"; 
  export let error = "";

  function handleInput(event) {
    const newValue = event.target.value.replace(/\D/g, '');
    inputValue = newValue;

    if (inputValue.length > maxLength) {
      error = `Длина не должна превышать ${maxLength} символов.`;
    } else {
      error = '';
    }
  }
</script>

<div class="input-field">
  <label for={`input-${label}`}>
    {label}
    {required ? "*" : ""}
  </label>

  {#if type === 'text'}
    <input
      type="text"
      bind:value={inputValue}
      placeholder={label}
      maxlength={maxLength}
      required={required}
      on:input={handleInput}
      id={`input-${label}`}
    />
  {/if}

  {#if type === 'email'}
    <input
      type="email"
      bind:value={inputValue}
      placeholder={label}
      maxlength={maxLength}
      required={required}
      on:input={handleInput}
      id={`input-${label}`}
    />
  {/if}

  {#if type === 'tel'}
    <input
      type="tel"
      bind:value={inputValue}
      placeholder={label}
      required={required}
      on:input={handleInput}
      id={`input-${label}`}
      maxlength={maxLength}
      title="Только цифры"
    />
  {/if}

  {#if error}
    <span class="error">{error}</span>
  {/if}
</div>

<style>
  .input-field {
    margin-bottom: 1rem;
    display: flex;
    flex-direction: column;
    width: 360px;
    gap: 10px;
  
  
  }
  @media (max-width: 450px) {
    .input-field {
      width: 100%;
    }
  }

  .input-field label {
    font-size: 15px;
    font-weight: 300;
    line-height: 18px;
    text-align: left;
    color: #797ea3;
  }

  .input-field input {
    border: none;
    background-color: rgba(0, 0, 0, 0);
    border-bottom: 1px solid #3F4363;
    padding-bottom: 5px;
    outline: none;
    font-size: 15px;
    font-weight: 300;
    line-height: 18px;
    text-align: left;
    color: #fff;
  }

  .input-field input:focus {
    border-bottom: 1px solid #fff;
    color: #fff;
  }

  .error {
    color: red;
    font-size: 0.875rem;
  }
</style>
