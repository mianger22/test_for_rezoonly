<template>
  <div class="form_container">
      <hr />
      <ContainerTitle />

      <div class="form_container__form"> 
        <div class="form_container__row">
          <FieldUserName 
            :username="form_data.user_name" 
            :error_print_username="input_errors.error_print_username" 
            :change_username="change_username" 
          />
          <FieldRole 
            :selecter_values="selecter_values" 
            :error_select_role="input_errors.error_select_role" 
            :change_jobtitle="change_jobtitle" 
          />
        </div>
        <div class="form_container__row">
          <FieldEmail 
            :email="form_data.email" 
            :error_print_email="input_errors.error_print_email" 
            :change_email="change_email" 
          />
        </div>
        <div class="form_container__row">
          <FieldPassword 
            :password="form_data.password" 
            :error_print_password="input_errors.error_print_password" 
            :change_password="change_password" 
          />
          <FieldRePassword 
            :repassword="form_data.repassword" 
            :error_print_repassword="input_errors.error_print_repassword" 
            :change_repassword="change_repassword" 
          />
        </div>

        <hr />
        <AgreementCheckBox :toggle_button_visible="toggle_button_visible" />
        <ButtonRegistration :disabled_button="disabled_button" :send_form_data="send_form_data" />
      </div>
    </div>
</template>

<script>
  import ContainerTitle from "./form/ContainerTitle.vue";
  import AgreementCheckBox from "./form/AgreementCheckBox.vue";
  import ButtonRegistration from "./form/ButtonRegistration.vue";
  import FieldUserName from "./form/fields/FieldUserName.vue";
  import FieldRole from "./form/fields/FieldRole.vue";
  import FieldEmail from "./form/fields/FieldEmail.vue";
  import FieldPassword from "./form/fields/FieldPassword.vue";
  import FieldRePassword from "./form/fields/FieldRePassword.vue";

  export default {
    name: 'FormDetail',
    components: {
      ContainerTitle,
      FieldUserName,
      FieldRole,
      FieldEmail,
      FieldPassword,
      FieldRePassword,
      AgreementCheckBox,
      ButtonRegistration
    },
    props: {
      disabled_button: Boolean,
      toggle_button_visible: Function,
      form_data: {
        user_name: String,
        email: String,
        password: String,
        repassword: String
      },
      selecter_values: Array,
      change_username: Function,
      change_jobtitle: Function,
      change_email: Function,
      change_password: Function,
      change_repassword: Function,
      send_form_data: Function,
      input_errors: {
        error_print_username: String,
        error_select_role: String,
        error_print_email: String,
        error_print_password: String,
        error_print_repassword: String,
      }
    }
  }
</script>

<style>
  .error_field {
    color: red;
    margin-top: 6px;
    margin-left: 2px;
    font-size: 12px;
  }

  .form_container__row {
    display: flex;
    margin-bottom: 25px;
  }
  
  .form_container__field {
    width: 450px;
    height: 39px;
    border-radius: 11px;
    border: 1px solid #E6E6EB;
    gap: 10px;
    display: flex;
    align-items: center;
    padding-left: 5px;
  }

  .form_container__field_container:not(:last-child) {
    margin-right: 18px;
  }

  .form_container__field input, .form_container__field select {
    font-size: 14px;
    font-weight: 400;
    line-height: 19px;
    letter-spacing: -0.0015em;
    text-align: left;
    border: none;
    width: 97%;
    outline: none;
  }

  hr {
    height: 1px;
    background-color: #D9D9D9;
    border: none;

    margin-top: 30.5px;
    margin-bottom: 25.5px;
  }

  hr:first-child {
    margin-top: 30px;
    margin-bottom: 20px;
  }

  /* изменил цвет placeholder`а */
  input::placeholder, 
  input::-webkit-input-placeholder, 
  input:-moz-placeholder, 
  input::-moz-placeholder, 
  input:-ms-input-placeholder {
    color: #9292A0;
    font-weight: 400;
  }
</style>
