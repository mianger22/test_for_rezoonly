<template>
  <div>
    <div v-if="!success_registration">
      <div class="title">
        Регистрация
      </div>
      <div class="container">
        <div class="toggle_visible_profile">
          <div class="toggle_visible_profile__switch">
            <input type="checkbox" id="checkbox_profile_visibility" name="checkbox_profile_visibility" checked="checked" @click="change_profile_visibility" />
            <label for="checkbox_profile_visibility" class="label_profile_visibility"></label>
            <label class="toggle_public_profile">
              Публичный профиль
            </label>
          </div>
          <div class="toggle_visible_profile__description">
            Включает профиль для просмотра другими пользователями по ссылке
          </div>
        </div>
        <FormDetail 
          :disabled_button="disabled_button"
          :toggle_button_visible="toggle_button_visible"
          :form_data="form_data" 
          :selecter_values="selecter_values" 
          :change_username="change_username"
          :change_jobtitle="change_jobtitle"
          :change_email="change_email"
          :change_password="change_password"
          :change_repassword="change_repassword"
          :send_form_data="send_form_data"
          :input_errors="input_errors"
        />
      </div>
    </div>
    <div v-else class="success_registration">
      <div class="success_registration_content">
        Регистрация успешно завершена
      </div>
    </div>
  </div>
</template>

<script>
  import FormDetail from "./components/FormDetail.vue";

  export default {
    name: 'App',
    components: {
      FormDetail
    },
    // дефолтные значения, которые отправлю компоненту формы, и там же их изменят и обновят данный массив данных, и отправлять будем из этого компонента значения из данного объекта
    data() {
      return {
        disabled_button: false,
        profile_visibility: "public",
        form_data: {
          user_name: "",
          job_title: "",
          email: "",
          password: "",
          repassword: ""
        },
        selecter_values: [{value: "Директор", name: "Директор"},{value: "Водитель", name: "Водитель"},{value: "Секретарь", name: "Секретарь"}],
        input_errors: {
          error_print_username: "",
          error_select_role: "",
          error_print_email: "",
          error_print_password: "",
          error_print_repassword: "",
        },
        success_registration: false
      }
    },
    methods: {
      toggle_button_visible() {
        // меняем доступность кнопки для нажатия
        this.disabled_button = !this.disabled_button;
      },
      change_profile_visibility() {
        if (this.profile_visibility === "public") {
          this.profile_visibility = "private";
        } else {
          this.profile_visibility = "public";
        }
      },
      change_username(new_username) {
        this.form_data.user_name = new_username;
      },
      change_jobtitle(new_jobtitle) {
        this.form_data.job_title = new_jobtitle;
        // меняю цвет названия выбранной роли
        document.querySelector("select").style.color = "black";
      },
      change_email(new_email) {
        this.form_data.email = new_email;
      },
      change_password(new_password) {
        this.form_data.password = new_password;
      },
      change_repassword(new_repassword) {
        this.form_data.repassword = new_repassword;
      },
      send_form_data() {
        const profile_visibility = this.profile_visibility === "public" ? 1 : 0;
        const username = this.form_data.user_name;
        const role = this.form_data.job_title;
        const email = this.form_data.email;
        const password = this.form_data.password;
        const password_repeat = this.form_data.repassword;

        async function create_profile(url, data) {
          const response = await fetch(url, { method: "POST", headers: {"Content-Type": "application/json"}, body: JSON.stringify(data) });
          
          return response.json(); 
        }
        
        if (username && role && email && password && password_repeat) {          
          create_profile("https://lmstestapi.reezonly.com/v1/user/signup", { public: profile_visibility, username, role, email, password, password_repeat }).then((profile_created) => {
            // если профиль успешно зарегистрирован, то показывать страницу с текстом о данном событии
            if (profile_created.success === true) this.success_registration = true
             
            // если нет, то
            const errors = profile_created.errors;

            for (let key in errors) {
              if (key === "username") {
                this.input_errors.error_print_username = errors[key][0];
              }

              if (key === "role") {
                this.input_errors.error_select_role = errors[key][0];
              }

              if (key === "email") {
                this.input_errors.error_print_email = errors[key][0];
              }

              if (key === "password") {
                this.input_errors.error_print_password = errors[key][0];
              }

              if (key === "password_repeat") {
                this.input_errors.error_print_repassword = errors[key][0];
              }
            }
          });
        } else {
          alert(" Заполните все поля! ")
        }
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;1,100;1,200;1,300;1,400;1,500&display=swap');

  body {
    font-family: Montserrat;
    margin: 0;
    padding: 0;
  }

  /* стили для показа текста после успешной регистрации */

  .success_registration {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .success_registration_content {
    display: inline-block;
  }

  /* стили страницы до успешной регистрации */

  .title {
    margin-top: 27px;
    font-size: 19px;
    font-weight: 900;
    line-height: 27px;
    letter-spacing: -0.0035em;
    text-align: left;
    width: 100%;
    height: 54px;
    gap: 27px;
    color: #000000;
    border-bottom: 1px solid #D9D9D9;
    padding-left: 20px;
  }

  .container {
    width: 958px;
    height: 638px;
    margin-left: 20px;
  }

  .toggle_visible_profile {
    margin-top: 27px;
    width: 904px;
    height: 53px;
    top: 27px;
    left: 20px;
    gap: 27px;
  }

  .toggle_visible_profile__switch {
    font-size: 16px;
    font-weight: 500;
    line-height: 19px;
    letter-spacing: 0em;
    text-align: left;
    color: #000000;
    display: flex;
    align-items: center;
  }

  .toggle_visible_profile__description {
    margin-top: 15px;
    font-size: 14px;
    font-weight: 400;
    line-height: 19px;
    letter-spacing: -0.0015em;
    text-align: left;
    color: #696977;
    width: 904px;
    height: 19px;
  }

  .toggle_public_profile {
    margin-left: 15px;
  }

  /* ------------------------------------------------------ Стили каастомного чекбокса -------------------------------------------------------- */

  /* скрываю стандартный чекбокс, чтоб заменить его своим */
  #checkbox_profile_visibility {       
    display: none;
  }
  
  /* добавляю плавность перемещения кружка */
  #checkbox_profile_visibility+.label_profile_visibility, #checkbox_profile_visibility+.label_profile_visibility::before, #checkbox_profile_visibility+.label_profile_visibility::after {
    transition: all .3s;
  }

  /* создаю серый эллипс чекбокса */
  #checkbox_profile_visibility+.label_profile_visibility {
    display: inline-block;
    position: relative;
    width: 39px;
    height: 19px;
    border-radius: 100px;
    border: 0.5px;
    cursor: pointer;
    background-color: #ccc;
  }

  /* создаю белый кружок чекбокса */
  #checkbox_profile_visibility+.label_profile_visibility::after {
    border-radius: 50%;
    content: '';
    position: absolute;
    width: 19px;
    height: 19px;
    background-color: #FDFDFD; 
    border: 0.5px solid #CDCED8;  
    top: -0.5px;         
  }

  /* когда чекбокс кликнут, кружок двигаем в правый конец */
  #checkbox_profile_visibility:checked+.label_profile_visibility::after {
    left: 20px;
  }
 
  /* создаю синий эллипс чекбокса */
  #checkbox_profile_visibility:checked+.label_profile_visibility {
    background-color: #7D7AFF;
    border: none;
  }
</style>
