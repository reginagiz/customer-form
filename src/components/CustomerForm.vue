<template>
  <form @submit.prevent="handleSubmit">
    <h2>Персональная информация</h2>
    <div class="field-container">
      <label for="surname">Фамилия*:</label>
      <input
        id="surname"
        v-model.trim="$v.form.surname.$model"
        :class="
          !$v.form.surname.required && formSubmitted
            ? 'red_input'
            : 'normal_input'
        "
        placeholder="Иванов"
      />
      <span class="error" v-if="!$v.form.surname.required && formSubmitted"
        >Обязательно к заполнению</span
      >
    </div>
    <div class="field-container">
      <label for="name">Имя*:</label>
      <input
        id="name"
        v-model.trim="$v.form.name.$model"
        :class="
          !$v.form.name.required && formSubmitted ? 'red_input' : 'normal_input'
        "
        placeholder="Иван"
      />
      <span class="error" v-if="!$v.form.name.required && formSubmitted"
        >Обязательно к заполнению</span
      >
    </div>
    <div class="field-container">
      <label for="patronymic">Отчество:</label>
      <input
        id="patronymic"
        v-model.trim="$v.form.patronymic.$model"
        class="normal_input"
        placeholder="Иванович"
      />
    </div>
    <div class="field-container">
      <label for="dob">Дата рождения*:</label>
      <input
        type="date"
        id="dob"
        v-model.trim="$v.form.dob.$model"
        :class="
          !$v.form.dob.required && formSubmitted ? 'red_input' : 'normal_input'
        "
      />
      <span class="error" v-if="!$v.form.dob.required && formSubmitted"
        >Обязательно к заполнению</span
      >
    </div>
    <div class="field-container">
      <label for="phone">Номер телефона*:</label>
      <input
        id="phone"
        v-model.trim="$v.form.phone_num.$model"
        :class="
          !$v.form.phone_num.required && formSubmitted
            ? 'red_input'
            : 'normal_input'
        "
        placeholder="79229925885"
      />
      <span v-if="$v.form.phone_num?.$pending">Validating...</span>
      <span v-if="$v.form.phone_num.$error && formSubmitted">
        Обязателен к заполнению, должен начинаться с 7 и иметь 11 цифр
      </span>
    </div>
    <div class="field-container">
      <label for="gender">Пол:</label>
      <select
        id="gender"
        v-model.trim="$v.form.gender.$model"
        class="normal_select"
      >
        <option value="" disabled selected>Выберите из списка</option>
        <option value="male">Мужской</option>
        <option value="female">Женский</option>
      </select>
    </div>
    <div class="field-container multiple-select">
      <label for="clientGroup">Группа клиентов*:</label>
      <select
        id="clientGroup"
        v-model.trim="$v.form.clientGroup.$model"
        multiple
        :class="
          !$v.form.clientGroup.required && formSubmitted
            ? 'red_select'
            : 'normal_select'
        "
      >
        <option value="VIP">VIP</option>
        <option value="Problematic">Проблемные</option>
        <option value="Compulsory Medical Insurance">ОМС</option>
      </select>
      <span class="error" v-if="!$v.form.clientGroup.required && formSubmitted"
        >Обязательно к заполнению</span
      >
    </div>
    <div class="field-container">
      <label for="attendingDoctor">Лечащий врач:</label>
      <select
        id="attendingDoctor"
        v-model.trim="$v.form.attendingDoctor.$model"
        class="normal_select"
      >
        <option value="" disabled selected>Выберите из списка</option>
        <option value="Ivanov">Иванов</option>
        <option value="Zakharov">Захаров</option>
        <option value="Chernysheva">Чернышева</option>
      </select>
    </div>
    <div class="checkbox">
      <label for="doNotSendSMS">Не отправлять СМС</label>
      <input
        id="doNotSendSMS"
        type="checkbox"
        v-model.trim="$v.form.doNotSendSMS.$model"
      />
    </div>

    <h2>Адресс</h2>
    <div class="field-container">
      <label for="index">Индекс:</label>
      <input
        v-model.trim="$v.form.address.index.$model"
        name="index"
        class="normal_input"
        placeholder="101000"
      />
    </div>
    <div class="field-container">
      <label for="country">Страна:</label>
      <input
        v-model.trim="$v.form.address.country.$model"
        name="country"
        class="normal_input"
        placeholder="Россия"
      />
    </div>
    <div class="field-container">
      <label for="region">Область:</label>
      <input
        v-model.trim="$v.form.address.region.$model"
        name="region"
        class="normal_input"
        placeholder="Московская"
      />
    </div>
    <div class="field-container">
      <label for="city">Город*:</label>
      <input
        v-model.trim="$v.form.address.city.$model"
        name="city"
        :class="
          !$v.form.address.city.required && formSubmitted
            ? 'red_input'
            : 'normal_input'
        "
        placeholder="Москва"
      />
      <span v-if="!$v.form.address.city.required && formSubmitted"
        >Обязательно к заполнению</span
      >
    </div>
    <div class="field-container">
      <label for="street">Улица:</label>
      <input
        v-model.trim="$v.form.address.street.$model"
        name="street"
        class="normal_input"
        placeholder="Ленина"
      />
    </div>
    <div class="field-container">
      <label for="house">Дом:</label>
      <input
        v-model.trim="$v.form.address.house.$model"
        name="house"
        class="normal_input"
        placeholder="67"
      />
    </div>

    <h2>Паспорт</h2>
    <div class="field-container">
      <label for="documentType">Тип документа*:</label>
      <select
        id="documentType"
        v-model.trim="$v.form.passport.documentType.$model"
        :class="
          !$v.form.passport.documentType.required && formSubmitted
            ? 'red_select'
            : 'normal_select'
        "
      >
        <option value="" disabled selected>Выберите из списка</option>
        <option value="Passport" selected>Паспорт</option>
        <option value="Birth Certificate">Свидетельство о рождении</option>
        <option value="Driver.ID">Вод. удостоверение</option>
      </select>
      <span
        class="error"
        v-if="!$v.form.passport.documentType.required && formSubmitted"
        >Обязательно к заполнению</span
      >
    </div>
    <div class="field-container">
      <label for="series">Серия:</label>
      <input
        id="series"
        v-model.trim="$v.form.passport.series.$model"
        class="normal_input"
        placeholder="72"
      />
    </div>
    <div class="field-container">
      <label for="number">Номер:</label>
      <input
        id="number"
        v-model.trim="$v.form.passport.number.$model"
        class="normal_input"
        placeholder="5637894"
      />
    </div>
    <div class="field-container">
      <label for="issuedBy">Кем выдан:</label>
      <input
        id="issuedBy"
        v-model.trim="$v.form.passport.issuedBy.$model"
        class="normal_input"
        placeholder="УФМС России города Москвы"
      />
    </div>
    <div class="field-container">
      <label for="dateOfIssue">Дата выдачи*:</label>
      <input
        type="date"
        id="dateOfIssue"
        v-model.trim="$v.form.passport.dateOfIssue.$model"
        :class="
          !$v.form.passport.dateOfIssue.required && formSubmitted
            ? 'red_input'
            : 'normal_input'
        "
      />
      <span
        class="error"
        v-if="!$v.form.passport.dateOfIssue.required && formSubmitted"
        >Обязательно к заполнению</span
      >
    </div>

    <button type="submit">Создать</button>
  </form>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";
import { validationMixin } from "vuelidate";

export default {
  mixins: [validationMixin],
  data() {
    return {
      form: {
        name: "",
        surname: "",
        patronymic: "",
        dob: "",
        phone_num: "",
        gender: "",
        clientGroup: [],
        attendingDoctor: "",
        doNotSendSMS: false,
        address: {
          index: "",
          country: "",
          region: "",
          city: "",
          street: "",
          house: "",
        },
        passport: {
          documentType: "",
          series: "",
          number: "",
          issuedBy: "",
          dateOfIssue: "",
        },
      },
      formSubmitted: false,
    };
  },
  validations: {
    form: {
      name: { required },
      surname: { required },
      patronymic: {},
      dob: { required },
      phone_num: {
        required,
        minLength: minLength(11),
        maxLength: maxLength(11),
        startsWithSeven(value) {
          return /^7/.test(value);
        },
      },
      gender: {},
      clientGroup: { required },
      attendingDoctor: {},
      doNotSendSMS: {},
      address: {
        index: {},
        country: {},
        region: {},
        city: {
          required,
        },
        street: {},
        house: {},
      },
      passport: {
        documentType: {
          required,
        },
        series: {},
        number: {},
        issuedBy: {},
        dateOfIssue: {
          required,
        },
      },
    },
  },
  methods: {
    handleSubmit() {
      this.formSubmitted = true;
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
        alert("Ошибка! Форма заполнена некорректно!");
      } else {
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
          alert("Новый клиент успешно создан!");
          console.log("Form data:", this.form);
        }, 500);
      }
    },
  },
};
</script>

<style lang="css">
form {
  width: 400px;
  margin: 0 auto;
  background-color: #f1f1f1;
  padding: 30px;
  border-radius: 20px;
  font-size: 20px;
}
.field-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  text-align: left;
}
.normal_input,
.normal_select {
  display: block;
  box-sizing: border-box;
  border: none;
  outline: none;
  border-bottom: 1px solid #ddd;
  border-radius: 20px;
  padding: 20px;
  margin: 10px 0 5px 0;
  width: 100%;
}
.red_input,
.red_select {
  display: block;
  box-sizing: border-box;
  outline: none;
  border: 1px solid red;
  border-radius: 20px;
  padding: 20px;
  margin: 10px 0 5px 0;
  width: 100%;
}
span {
  color: red;
  font-size: 18px;
  text-align: left;
}
button {
  background-color: #3498db;
  padding: 20px 20px;
  margin-top: 30px;
  border: none;
  color: white;
  width: 100%;
  border-radius: 20px;
  text-transform: uppercase;
  font-weight: bold;
  letter-spacing: 2px;
}
.checkbox {
  display: flex;
}
.checkbox label {
  margin-right: 10px;
}
.checkbox input {
  width: 18px;
  height: 18px;
}
input,
select,
select option,
input::placeholder {
  font-size: 18px;
}
.multiple-select option {
  margin-bottom: 10px;
}
.multiple-select select {
  background-image: none;
}
select {
  appearance: none;
  background-image: url("data:image/svg+xml;utf8,<svg fill='black' height='24' viewBox='0 0 24 24' width='24' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/><path d='M0 0h24v24H0z' fill='none'/></svg>");
  background-repeat: no-repeat;
  background-position-x: 95%;
  background-position-y: center;
}
</style>
