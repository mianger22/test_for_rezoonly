<template>
  <div class="form_container__field_container">
    <div class="form_container__field">
      <input 
        type="password" 
        :value="repassword" 
        placeholder="Повторите пароль" 
        @input="event => change_repassword(event.target.value)" 
      />
    </div>
    <div v-if="error_print_repassword" class="error_field">{{ error_print_repassword }}</div>
  </div>
</template>

<script>
  export default {
    name: 'FieldRePassword',
    props: {
      repassword: String,
      error_print_repassword: String,
      change_repassword: Function
    }
  }
</script>

<style></style>