<template>
  <div class="main">
    <div class="form">
      <div class="title">
        <h1>Регистрация клиента</h1>
      </div>
      <form @submit.prevent="onSubmit">
        <div class="form-client">
          <div class="personal-date">
            <fieldset>
              <legend>Личные данные</legend>

              <!-- фамилия -->
              <div class="form-group">
                <div class="label">
                  <label for="surname"><b>Фамилия*</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Фамилия"
                    id="surname"
                    type="text"
                    v-model.trim="v$.form.surname.$model"
                    required
                  />
                  <!-- Error Message -->
                  <div
                    class="input-errors"
                    v-for="(error, index) of v$.form.surname.$errors"
                    :key="index"
                  >
                    <div class="error-msg">{{ error.$message }}</div>
                  </div>
                </div>
              </div>

              <!-- имя -->
              <div class="form-group">
                <div class="label">
                  <label for="name"><b>Имя*</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Имя"
                    id="name"
                    type="text"
                    v-model.trim="v$.form.name.$model"
                    required
                  />
                  <!-- Error Message -->
                  <div
                    class="input-errors"
                    v-for="(error, index) of v$.form.name.$errors"
                    :key="index"
                  >
                    <div class="error-msg">{{ error.$message }}</div>
                  </div>
                </div>
              </div>

              <!-- отчество -->
              <div class="form-group">
                <div class="label">
                  <label for="middlename"><b>Отчество</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Отчество"
                    id="middlename"
                    type="text"
                    v-model.trim="v$.middlename.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.middlename.$error">
                    Неверный формат ввода. Допустим ввод только букв
                  </div>
                </div>
              </div>

              <!-- дата рождения -->
              <div class="form-group">
                <div class="label">
                  <label for="birthdate"><b>Дата рождения*</b></label>
                </div>
                <div class="input">
                  <input
                    type="date"
                    placeholder="Дата рождения"
                    name="birthdate"
                    v-model.trim="v$.form.birthdate.$model"
                    required
                  />
                </div>
              </div>

              <!-- номер телефона -->
              <div class="form-group">
                <div class="label">
                  <label for="phone"><b>Номер телефона*</b></label>
                </div>
                <input
                  class="form-control"
                  id="phone"
                  type="tel"
                  placeholder="+79555555555"
                  maxlength="12"
                  v-model.trim="v$.form.phone.$model"
                  required
                />
                <!-- Error Message -->
                <div
                  class="input-errors"
                  v-for="(error, index) of v$.form.phone.$errors"
                  :key="index"
                >
                  <div class="error-msg">{{ error.$message }}</div>
                </div>
              </div>

              <!-- пол -->
              <div class="form-group">
                <div class="label">
                  <label for="gender"><b>Пол</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Пол"
                    id="gender"
                    type="text"
                    v-model.trim="v$.gender.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.gender.$error">
                    Неверный формат ввода. Допустим ввод только букв
                  </div>
                </div>
              </div>

              <div class="selected">
                <!-- группа клиентов -->
                <div class="form-group">
                  <div class="label">
                    <label for="clientsgroups"> Группа клиентов*</label>
                  </div>
                  <div class="input">
                    <select
                      id="clienstgroups"
                      class="form-control"
                      v-model="clientgroup"
                      multiple
                    >
                      <option
                        v-for="(clientgroup, index) in clientsgroups"
                        v-bind:value="clientgroup.value"
                        :key="index"
                      >
                        {{ clientgroup.label }}
                      </option>
                    </select>
                  </div>
                </div>

                <!-- лечащий врач -->
                <div class="form-group">
                  <div class="label">
                    <label for="doctor">Лечащий врач:</label>
                  </div>
                  <div class="input">
                    <select id="doc" class="form-control" v-model="doctor">
                      <option
                        v-for="(doctor, index) in doctors"
                        v-bind:value="doctor.value"
                        :key="index"
                      >
                        {{ doctor.label }}
                      </option>
                    </select>
                  </div>
                </div>
              </div>

              <!-- не отправлять смс -->
              <div class="form-check">
                <input
                  type="checkbox"
                  id="notification"
                  class="form-check-input"
                  v-model="notAgreeSms"
                />
                <label class="form-check-label" for="notification"
                  >Не отправлять СМС</label
                >
              </div>
            </fieldset>
          </div>

          <!--АДРЕС-->
          <div class="address">
            <fieldset>
              <legend>Адрес</legend>

              <!-- Индекс -->
              <div class="form-group">
                <div class="label">
                  <label for="postcode"><b>Индекс</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Индекс"
                    id="postcode"
                    type="text"
                    maxlength="6"
                    v-model.trim="v$.postcode.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.postcode.$error">
                    Допустим ввод только 6 цифр
                  </div>
                </div>
              </div>

              <!-- Страна -->
              <div class="form-group">
                <div class="label">
                  <label for="country"><b>Страна</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Страна"
                    id="country"
                    type="text"
                    v-model.trim="v$.country.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.country.$error">
                    Неверный формат ввода. Допустим ввод только букв
                  </div>
                </div>
              </div>
              <!--Область-->
              <div class="form-group">
                <div class="label">
                  <label for="area"><b>Область</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Область"
                    id="area"
                    type="text"
                    v-model.trim="v$.area.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.area.$error">
                    Неверный формат ввода. Допустим ввод только букв
                  </div>
                </div>
              </div>

              <!--Город-->
              <div class="form-group">
                <div class="label">
                  <label for="city"><b>Город*</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Город"
                    id="city"
                    type="text"
                    v-model.trim="v$.form.city.$model"
                    required
                  />
                  <!-- Error Message -->
                  <div
                    class="input-errors"
                    v-for="(error, index) of v$.form.city.$errors"
                    :key="index"
                  >
                    <div class="error-msg">{{ error.$message }}</div>
                  </div>
                </div>
              </div>

              <!--Улица-->
              <div class="form-group">
                <div class="label">
                  <label for="street"><b>Улица</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Улица"
                    id="street"
                    type="text"
                    v-model.trim="v$.street.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.street.$error">
                    Неверный формат ввода. Допустим ввод только букв
                  </div>
                </div>
              </div>

              <!--Дом-->
              <div class="form-group">
                <div class="label">
                  <label for="house"><b>Дом</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Дом"
                    id="house"
                    type="text"
                    v-model.trim="v$.house.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.house.$error">
                    Неверный формат ввода. Допустим ввод только цифр
                  </div>
                </div>
              </div>
            </fieldset>
          </div>

          <!--ПАСПОРТНЫЕ ДАННЫЕ-->
          <div class="passport">
            <fieldset>
              <legend>Паспортные данные</legend>
              <div class="form-group">
                <!--Тип документа-->
                <div class="label">
                  <label for="typedoc">Тип документа*:</label>
                </div>
                <div class="input">
                  <select id="typedoc" class="form-control" v-model="typedoc">
                    <option
                      v-for="(typedoc, index) in typesdocs"
                      v-bind:value="typedoc.value"
                      :key="index"
                    >
                      {{ typedoc.label }}
                    </option>
                  </select>
                </div>
              </div>

              <!--Серия-->
              <div class="form-group">
                <div class="label">
                  <label for="series"><b>Серия</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Серия"
                    id="series"
                    type="text"
                    maxlength="4"
                    v-model.trim="v$.series.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.series.$error">
                    Неверный формат ввода. Допустим ввод только цифр
                  </div>
                </div>
              </div>

              <!--Номер-->
              <div class="form-group">
                <div class="label">
                  <label for="numberpass"><b>Номер</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Номер"
                    id="numberpass"
                    type="text"
                    maxlength="6"
                    v-model.trim="v$.numberpass.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.numberpass.$error">
                    Неверный формат ввода. Допустим ввод только цифр
                  </div>
                </div>
              </div>

              <!--Кем выдан-->
              <div class="form-group">
                <div class="label">
                  <label for="issued"><b>Кем выдан</b></label>
                </div>
                <div class="input">
                  <input
                    class="form-control"
                    placeholder="Кем выдан"
                    id="issued"
                    type="text"
                    v-model.trim="v$.issued.$model"
                  />
                  <!-- Error Message -->
                  <div class="input-errors" v-if="v$.issued.$error">
                    Неверный формат ввода. Допустим только буквенный ввод
                  </div>
                </div>
              </div>

              <!--Дата выдачи-->
              <div class="form-group">
                <div class="label">
                  <label for="dateissued"><b>Дата выдачи*</b></label>
                </div>
                <div class="input">
                  <input
                    type="date"
                    placeholder="Дата выдачи"
                    name="dateissued"
                    v-model.trim="v$.form.dateissued.$model"
                    required
                  />
                </div>
              </div>
            </fieldset>
          </div>
        </div>
      </form>
      <div class="reg-button">
        <button
          class="show-modal-window"
          @click="showModal"
          :disabled="v$.form.$invalid"
        >
          Зарегистрировать
        </button>

        <modal-window ref="modal"></modal-window>
      </div>
    </div>
  </div>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, minLength, maxLength } from "@vuelidate/validators";

import ModalWindow from "./ModalWindow.vue";

export function validText(text) {
  let validNamePattern = new RegExp(
    "^[а-яa-zЁёА-ЯA-Z]+(?:[-'\\s][а-яa-zЁёА-ЯA-Z]+)*$"
  );
  if (validNamePattern.test(text)) {
    return true;
  }
  return false;
}

export function validNumberSix(numbers) {
  let validPostcodePattern = new RegExp("^\\d{6}$");
  if (validPostcodePattern.test(numbers)) {
    return true;
  }
  return false;
}

export function validNumberFour(numbers) {
  let validPostcodePattern = new RegExp("^\\d{4}$");
  if (validPostcodePattern.test(numbers)) {
    return true;
  }
  return false;
}

export function validNumberOnly(numbers) {
  let validPostcodePattern = new RegExp("^\\d$");
  if (validPostcodePattern.test(numbers)) {
    return true;
  }
  return false;
}

export function validNumberPhone(phone) {
  let validNumberPhonePattern = new RegExp("^\\+79\\d{9}$");
  if (validNumberPhonePattern.test(phone)) {
    return true;
  }
  return false;
}

export default {
  name: "App",
  components: {
    ModalWindow,
  },
  methods: {
    showModal: function () {
      this.$refs.modal.show = true;
    },
  },
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      error: "",
      gender: "",
      country: "",
      area: "",
      street: "",
      house: "",
      series: "",
      numberpass: "",
      issued: "",
      notAgreeSms: false,
      doctor: "Ivanov",
      doctors: [
        {
          label: "Иванов",
          value: "Ivanov",
        },
        {
          label: "Захаров",
          value: "Zakharov",
        },
        {
          label: "Чернышева",
          value: "Chernysheva",
        },
      ],
      typedoc: "Passport",
      typesdocs: [
        {
          label: "Паспорт",
          value: "Passport",
        },
        {
          label: "Свидетельство о рождении",
          value: "Birth certificate",
        },
        {
          label: "Водителеськое удостоверение",
          value: "Driver's license",
        },
      ],
      middlename: "",
      postcode: "",
      clientgroup: ["VIP"],
      clientsgroups: [
        {
          label: "VIP",
          value: "VIP",
        },
        {
          label: "Проблемные",
          value: "Trouble",
        },
        {
          label: "ОМС",
          value: "OMC",
        },
      ],

      form: {
        city: "",
        surname: "",
        name: "",
        birthdate: "",
        phone: "",
        dateissued: "",
      },
    };
  },
  validations() {
    return {
      isModalVisible: false,
      series: {
        maxLength: maxLength(4),
        series_valid: {
          $validator: validNumberFour,
        },
      },
      numberpass: {
        maxLength: maxLength(6),
        numberpass_valid: {
          $validator: validNumberSix,
        },
      },
      issued: {
        issued_valid: {
          $validator: validText,
        },
      },
      house: {
        house_valid: {
          $validator: validNumberOnly,
        },
      },
      area: {
        area_valid: {
          $validator: validText,
        },
      },
      gender: {
        gender_valid: {
          $validator: validText,
        },
      },
      middlename: {
        middlename_valid: {
          $validator: validText,
        },
      },
      country: {
        country_valid: {
          $validator: validText,
        },
      },
      street: {
        street_valid: validText,
      },
      postcode: {
        maxLength: maxLength(6),
        minLength: minLength(6),
        zip_valid: {
          $validator: validNumberSix,
        },
      },
      form: {
        surname: {
          required,
          minLength: minLength(2),
          name_validation: {
            $validator: validText,
            $message:
              "Неверный ввод данных. Допустимы только буквы, тире и пробелы",
          },
        },
        name: {
          required,
          minLength: minLength(2),
          name_validation: {
            $validator: validText,
            $message:
              "Неверный ввод данных. Допустимы только буквы, тире и пробелы",
          },
        },
        birthdate: {
          required,
        },
        dateissued: {
          required,
        },
        phone: {
          minLength: { minLength: minLength(12) },
          maxLength: { maxLength: maxLength(12) },
          required,
          phone_valid: {
            $validator: validNumberPhone,
            $message:
              "Введен неверный формат номера телефона. Номер должен начинаться с +7",
          },
        },
        city: {
          required,
          minLength: minLength(2),
          name_validation: {
            $validator: validText,
            $message:
              "Неверный ввод данных. Допустимы только буквы, тире и пробелы",
          },
        },
      },
    };
  },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500&display=swap");

$colorBackForm: #f5e9d9;
$colorAdditionalPink: #c42061;
$colorGeneralPink: #f67ca5;
$colorWarning: #ff0000;
$colortxt: #605756;
$colorFieldsetBack: #fffdee;
$fontGeneral: "Playfair Display";

@mixin breakpoint($point) {
  @if $point == sm {
    @media (max-width: 576px) {
      @content;
    }
  } @else if $point == md {
    @media (max-width: 768px) {
      @content;
    }
  }
}

form {
  background: $colorBackForm;

  .form-client {
    display: flex;
    text-align: center;
    align-items: flex-start;
    padding-bottom: 25px;
    justify-content: space-evenly;

    fieldset {
      max-width: 350px;
      margin: 50px auto 0;
      padding: 20px;
      background: $colorFieldsetBack;
      border: 10px solid transparent;
      font-family: $fontGeneral;
      color: $colortxt;
      border-radius: 20px;
      border: solid 5px $colorGeneralPink;

      legend {
        font-family: $fontGeneral;
        font-size: 22px;
      }
      .form-group {
        font-family: $fontGeneral;
        color: $colortxt;

        .label {
          padding-bottom: 10px;
          padding-top: 10px;
        }

        input {
          width: 100%;
          padding: 0 10px;
          line-height: 35px;
          border-width: 0;
          outline: none;
          background: transparent
            url(https://html5book.ru/wp-content/uploads/2016/12/bg-form.png)
            bottom left repeat-x;
          background-size: 8px 35px;
          font-family: $fontGeneral;
        }

        select {
          background-color: $colorBackForm;
          border: 2px solid $colorGeneralPink;
          border-radius: 7px;
          font-family: $fontGeneral;
          font-size: 15px;
        }
      }

      .form-check {
        display: inline-flex;
        justify-content: space-evenly;
        align-items: center;
        padding-top: 15px;
      }
    }
  }

  @include breakpoint(md) {
    .form-client {
      flex-direction: column;
      align-items: center;
    }
  }

  @include breakpoint(sm) {
    .form-client {
      flex-direction: column;
      align-items: center;
    }
  }
}

.reg-button {
  text-align: center;
}

.address,
.passport,
.personal-date {
  margin: 5px;
  padding: 5px;
  flex: 0 1 auto;
}

h1 {
  text-align: center;
  font-family: $fontGeneral;
}

input:invalid {
  border-bottom: 5px solid $colorAdditionalPink;
}

.show-modal-window {
  padding: 10px 20px;
  margin-top: 10px;
  background: $colorGeneralPink;
  border-width: 0;
  cursor: pointer;
  outline: none;
  font-family: $fontGeneral;
  font-size: 13px;
  letter-spacing: 1px;
  color: $colorFieldsetBack;
  text-transform: uppercase;
  transition: 1s cubic-bezier(0.165, 0.84, 0.44, 1);
}
.show-modal-window:hover {
  background: $colorAdditionalPink;
}

.input-errors {
  color: $colorWarning;
  font-weight: bold;
}

.error-msg {
  color: $colorWarning;
  font-weight: bold;
}

.selected {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}
</style>