<template>
  <div class="form_container__field_container">
    <div class="form_container__field">
      <input type="text" :value="username" placeholder="Имя" @input="event => change_username(event.target.value)" />
    </div>
    <div v-if="error_print_username" class="error_field">{{ error_print_username }}</div>
  </div>
</template>

<script>
  export default {
    name: 'FieldUserName',
    props: {
      username: String,
      error_print_username: String,
      change_username: Function
    }
  }
</script>

<style></style>