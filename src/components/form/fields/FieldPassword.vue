<template>
  <div class="form_container__field_container">
    <div class="form_container__field">
      <input type="password" :value="password" placeholder="Пароль" @input="event => change_password(event.target.value)" />
    </div>
    <div v-if="error_print_password" class="error_field">{{ error_print_password }}</div>
  </div>
</template>

<script>
  export default {
    name: 'FieldPassword',
    props: {
      password: String,
      error_print_password: String,
      change_password: Function
    }
  }
</script>

<style></style>