<script>
	import toast, { Toaster } from "svelte-french-toast";
	import Checkbox from "./components/Checkbox/Checkbox.svelte";
	import InputField from "./components/InputField/InputField.svelte";
	import SubmitButton from "./components/SubmitButton/SubmitButton.svelte";
  
	let formData = {
	  name: "",
	  company: "",
	  email: "",
	  phone: "",
	  subject: "",
	  message: "",
	  agree: false
	};
	
	let errors = {};
  
	function showToast(type, message) {
	  toast[type](message, {
		duration: 5000,
		position: "top-center",
		closeButton: true,
	  });
	}
  
	function validateForm() {
	  errors = {};
	  if (!formData.name) errors.name = "Имя обязательно";
	  if (!formData.company) errors.company = "Компания обязательна";
	  if (!formData.email || !/\S+@\S+\.\S+/.test(formData.email)) errors.email = "Некорректный email";
	  if (!formData.message) errors.message = "Сообщение обязательно";
	  if (!formData.agree) errors.agree = "Необходимо согласиться с условиями";
	  return Object.keys(errors).length === 0;
	}
  
	
	function handleSubmit() {
	  if (validateForm()) {
		showToast("success", "Данные успешно отправлены!");  
	    errors = {};
	  } else {
		showToast("error", "Произошла ошибка, попробуйте снова.");
	  }
	}
  </script>
  
  <div class="container">
	<h1>hello</h1>
	<form on:submit|preventDefault={handleSubmit}>
	  <p class="title">For business enquiries please<br /> use the form below</p>
	  <span>* обязательные поля</span>
  
	  {#each [
		{ label: "Имя", key: "name", required: true, type: "text", minLength: 2, maxLength: 30 },
		{ label: "Компания", key: "company", required: true, type: "text", minLength: 2, maxLength: 50 },
		{ label: "E-mail", key: "email", required: true, type: "email" },
		{ label: "Телефон", key: "phone", required: true, type: "tel", minLength: 17, maxLength: 17 },
		{ label: "Тема", key: "subject", required: true, type: "text", minLength: 5, maxLength: 100 },
		{ label: "Сообщение", key: "message", required: true, type: "text", minLength: 10, maxLength: 500 }
	  ] as { label, key, required, type, minLength, maxLength }}
		<InputField
		  label={label}
		  value={formData[key]}
		  required={required}
		  type={type}
		  minLength={minLength}
		  maxLength={maxLength}
		  onInput={(e) => (formData[key] = e.target.value)}
		  error={errors[key]}
		  id={`${key}-input`}
		/>
	  {/each}
	  
	  <Checkbox
		label="Я согласен с условиями"
		checked={formData.agree}
		onChange={(e) => (formData.agree = e.target.checked)}
		error={errors.agree}
		id="agree-checkbox"
	  />
	  <SubmitButton label="Send" color="green" />
	  <Toaster />
	</form>
  </div>
  
  <style>
	form {
	  max-width: 600px;
	  padding: 40px 45px;
	  gap: 10px;
	  border-radius: 27px;
	  background-color: #171929;
	  display: flex;
	  flex-direction: column;
	}
	span {
	  margin: 0 auto;
	  padding: 0;
	  font-size: 15px;
	  font-weight: 300;
	  line-height: 18px;
	  color: #797ea3;
	  text-align: center;
	}
	.title {
	  margin: 0 auto;
	  padding: 0;
	  font-size: 18px;
	  font-weight: 400;
	  line-height: 21.6px;
	  text-align: center;
	  color: #ffffff;
	}
	.container {
	  max-width: 390px;
	  width: 100%;
	  margin: 0 auto;
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	  gap: 20px;
	}
	.container h1 {
	  color: #ffffff;
	  font-size: 55px;
	  font-weight: 500;
	  line-height: 66px;
	  text-align: center;
	  margin: 0;
	  padding: 0;
	}
  </style>
  