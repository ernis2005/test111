<script>
  import toast, { Toaster } from "svelte-french-toast";
  import Checkbox from "./components/Checkbox/Checkbox.svelte";
  import InputField from "./components/InputField/InputField.svelte";
  import SubmitButton from "./components/SubmitButton/SubmitButton.svelte";

  let name = "";
  let company = "";
  let email = "";
  let phone = "";
  let subject = "";
  let message = "";
  let agree = false;
  let errors = {};

  function showSuccessToast() {
    toast.success("Данные успешно отправлены!", {
      duration: 3000,
      position: "top-center",
      closeButton: true,
    });
  }

  function showErrorToast() {
    toast.error("Произошла ошибка, попробуйте снова.", {
      duration: 3000,
      position: "top-center",
      closeButton: true,
    });
  }
  function validateForm() {
    errors = {};
    if (!name) errors.name = "Имя обязательно";
    if (!company) errors.company = "Компания обязательна";
    if (!email || !/\S+@\S+\.\S+/.test(email))
      errors.email = "Некорректный email";
    if (!message) errors.message = "Сообщение обязательно";
    if (!agree) errors.agree = "Необходимо согласиться с условиями";
    return Object.keys(errors).length === 0;
  }

  function handleSubmit() {
    if (validateForm()) {
      showSuccessToast();
   
      errors = {};
    } else {
      showErrorToast();
    }
  }
</script>

<div class="container">
  <h1>hello</h1>
  <form on:submit|preventDefault={handleSubmit}>
    <p class="title">For business enquiries please<br /> use the form below</p>
    <span>* обязательные поля</span>
    <InputField
      label="Имя"
      value={name}
      required
      minLength={2}
      maxLength={30}
      onInput={(e) => (name = e.target.value)}
      error={errors.name}
      id="name-input"
    />

    <InputField
      label="Компания"
      value={company}
      required
      minLength={2}
      maxLength={50}
      onInput={(e) => (company = e.target.value)}
      error={errors.company}
      id="company-input"
    />

    <InputField
      label="E-mail"
      type="email"
      value={email}
      required
      onInput={(e) => (email = e.target.value)}
      error={errors.email}
	  minLength={5}
	  maxLength={150}
      id="email-input"
    />

    <InputField
      label="Телефон"
      required

	  type="tel"
      value={phone}
      minLength={17}
      maxLength={17}
      onInput={(e) => (phone = e.target.value)}
      error={errors.phone}
      id="phone-input"
    />

    <InputField
      label="Тема"
      value={subject}
      minLength={5}
      required

	  maxLength={100}
      onInput={(e) => (subject = e.target.value)}
      id="subject-input"
    />

    <InputField
      label="Сообщение"
      value={message}
      required

      minLength={10}
      maxLength={500}
      onInput={(e) => (message = e.target.value)}
      error={errors.message}
      id="message-input"
    />
	<Checkbox
      label="Я согласен с условиями"
      checked={agree}
      onChange={(e) => (agree = e.target.checked)}
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

    padding: 40px 45px 40px 45px;
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
