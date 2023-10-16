<template>
  <div class="form_container__field_container">
    <div class="form_container__field">
      <input type="text" :value="email" placeholder="Email" @input="event => change_email(event.target.value)" />
    </div>
    <div v-if="error_print_email" class="error_field">{{ error_print_email }}</div>
  </div>
</template>

<script>
  export default {
    name: 'FieldEmail',
    props: {
      email: String,
      error_print_email: String,
      change_email: Function
    }
  }
</script>

<style></style>