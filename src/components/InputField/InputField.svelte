<script>
  export let label = "";
  export let type = "text"; 
  export let value = "";
  export let required = false;
  export let minLength = 0;
  export let maxLength = Infinity;
  export let onInput;  
  export let error = "";

  let inputValue = value;

 function handleInput(event) {
   inputValue = event.target.value;
 
   if (onInput) onInput(event);
 
   if (type === 'tel') {
     inputValue = inputValue.replace(/\D/g, '');
     if (inputValue.length < minLength || inputValue.length > maxLength) {
       error = `Номер телефона должен содержать от ${minLength} до ${maxLength} цифр.`;
     } else {
       error = '';
     }
   } else {
     if (inputValue.length < minLength || inputValue.length > maxLength) {
       error = `Длина должна быть от ${minLength} до ${maxLength} символов.`;
     } else {
       error = '';
     }
   }
 }
</script>

<div class="input-field">
  <label for="input-{label}">
    {label}
    {required ? "*" : ""}
  </label>
  {#if type === 'text'}
    <input
      type="text"
      bind:value={inputValue}
      placeholder={label}
      maxlength={maxLength}
      minlength={minLength}
      {required}
      on:input={handleInput}
      id="input-{label}"
    />
  {/if}
                                     
  {#if type === 'email'}
    <input
      type="email"
      bind:value={inputValue}
      placeholder={label}
      {required}
      on:input={handleInput}
      id="input-{label}"
    />
  {/if}

  {#if type === 'tel'}
    <input
      type="tel"
      bind:value={inputValue}
      placeholder={label}
      {required}
      on:input={handleInput}
      id="input-{label}"

      maxlength="17"
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





