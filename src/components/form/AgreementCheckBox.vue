<template>
  <div class="form_container__agreement">
    <label class="container_checkbox">
      <input type="checkbox" checked="checked" class="checkbox_agreement" @click="toggle_button_visible">
      <span class="span_agreement"></span>
    </label>
    <label for="subscribeNews">
      Нажимая на кнопку "Регистрация", я подтверждаю своё согласие с политикой конфиденциальности и обработки персональных данных
    </label>
  </div>
</template>

<script>
  export default {
    name: 'AgreementCheckBox',
    props: {
      toggle_button_visible: Function,
    }
  }
</script>

<style>
  .form_container__agreement {
    width: 716px;
    height: 78px;
    top: 398px;
    left: 20px;
    border-radius: 5px;
    margin-top: 25.5px;
    display: flex;
  }

  .form_container__agreement label {
    height: 78px;
    top: 398px;
    left: 54px;
    font-size: 14px;
    font-weight: 410;
    line-height: 19px;
    letter-spacing: -0.0015em;
    text-align: left;
    color: #000000;
    margin-right: 10px;
  }
  
  /* скрываем дефолтный флажок */
  .container_checkbox .checkbox_agreement {
    opacity: 0;
  }

  label:first-child {
    margin-top: -22px;
  }

  /* создаём кастомный checkbox */
  .span_agreement {
    content: url("../../assets/checkbox_icon_off.svg");
    cursor: pointer;
  }

  /* когда отмечен, то меняем иконку на заполненную */
  .container_checkbox .checkbox_agreement:checked ~ .span_agreement {
    content: url("../../assets/checkbox_icon_on.svg");
  }
</style>