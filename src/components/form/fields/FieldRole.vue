<template>
  <div class="form_container__field_container">
    <div class="form_container__field">
      <select required @change="event => change_jobtitle(event.target.value)">
        <option value="" disabled selected hidden>Должность</option>
        <option v-for="(selecter_value, index) in selecter_values" :value="selecter_value.value" :key="index">
          {{ selecter_value.name }}
        </option>
      </select>
    </div>
    <div v-if="error_select_role" class="error_field">{{ error_select_role }}</div>
  </div>
</template>

<script>
  export default {
    name: 'FieldRole',
    props: {
      error_select_role: String,
      change_jobtitle: Function,
      selecter_values: Array,
    }
  }
</script>

<style>
  .form_container__field select {
    cursor: pointer;
    color: #9292A0; 
    font-weight: 400;
  }
</style>