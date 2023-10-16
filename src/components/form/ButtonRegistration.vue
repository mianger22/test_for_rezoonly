<template>
  <div class="form_container__button_registration">
    <div v-if="disabled_button" style="opacity: 0.3; cursor: not-allowed;">Регистрация</div>
    <div v-else @click="send_form_data">Регистрация</div>
  </div>
</template>

<script>
  export default {
    name: 'ButtonRegistration',
    props: {
      send_form_data: Function,
      disabled_button: Boolean
    }
  }
</script>

<style>
  .form_container__button_registration {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .form_container__button_registration div {
    font-size: 14px;
    font-weight: 500;
    line-height: 19px;
    letter-spacing: -0.0015em;
    text-align: left;
    padding: 10px 12px;
    border-radius: 9px;
    gap: 5px;
    color: #07A86E;
    border: 1.5px solid #07A86E;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 234px;
    cursor: pointer;
    user-select: none;
  }
</style>