<template>
  <div class="form-wrapper">
    <div v-if="title" class="form-title">{{ title }}</div>
    <div v-if="attention" class="attention">{{ attention }}</div>
    <form action="" class="form" :name="name">
      <Input
        type="text"
        name="name"
        placeholder="Имя*"
        :class="{ error: !form.name.valid }"
        v-model="form.name.value"
        @blur="validInput(form.name)"
        @focus="focusHandler(form.name)"
        required
      />
      <Input
        type="text"
        name="surname"
        placeholder="Фамилия*"
        :class="{ error: !form.surname.valid }"
        v-model="form.surname.value"
        @blur="validInput(form.surname)"
        @focus="focusHandler(form.surname)"
        required
      />
      <Input
        type="email"
        name="email"
        placeholder="Email*"
        :class="{ error: !form.email.valid }"
        v-model="form.email.value"
        @blur="validInput(form.email)"
        @focus="focusHandler(form.email)"
        required
      />
      <Input
        type="tel"
        name="phone"
        placeholder="Телефон*"
        :class="{ error: !form.phone.valid }"
        @keydown="phoneMaskHandler"
        v-model="form.phone.value"
        @blur="validInput(form.phone)"
        @focus="focusHandler(form.phone)"
        required
      />
      <Input
        type="date"
        name="birthday"
        placeholder="Дата рождения"
        v-model="form.birthday"
      />
      <Select
        :options="[
          { value: 'male', title: 'Мужской' },
          { value: 'female', title: 'Женский' },
        ]"
        name="gender"
        caption="Пол"
        v-model="form.gender"
      />
      <Checkbox
        name="privacy"
        id="privacy"
        required
        v-model="form.privacy"
        caption="*Согласен с ..."
      />
      <Button
        :disabled="!validForm"
        caption="Отправить"
        @onClick="$emit('onSubmit', sendFormHandler())"
      />
    </form>
  </div>
</template>
<script>
import Input from "../input/Input.vue";
import Button from "../button/Button.vue";
import Select from "../select/Select.vue";
import Checkbox from "../checkbox/Checkbox.vue";

export default {
  name: "Form",
  components: { Input, Button, Select, Checkbox },
  props: {
    name: {
      type: String,
      default: null,
    },
    title: {
      type: String,
      default: null,
    },
    attention: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      form: {
        name: {
          type: "text",
          value: "",
          valid: true,
        },
        surname: {
          type: "text",
          value: "",
          valid: true,
        },
        phone: {
          type: "tel",
          value: "",
          valid: true,
        },
        email: {
          type: "email",
          value: "",
          valid: true,
        },
        birthday: "",
        gender: "",
        privacy: false,
      },
      isSend: false,
    };
  },
  computed: {
    validForm() {
      let valid = true;

      if (!this.form.name.value || this.form.name.value.length < 2)
        valid = false;
      if (!this.form.surname.value || this.form.surname.value.length < 2)
        valid = false;
      if (!this.form.email.value || this.form.email.value.length < 6)
        valid = false;
      if (!this.form.phone.value || this.form.phone.value.length < 10)
        valid = false;
      if (!this.form.privacy) valid = false;

      return valid;
    },
  },
  methods: {
    sendFormHandler() {
      return { name: this.form.name.value, valid: this.validForm };
    },
    validInput(e) {
      switch (e.type) {
        case "text":
          if (!e.value || e.value.length < 2) e.valid = false;
          break;
        case "email":
          if (!e.value || e.value.length < 6) e.valid = false;
          break;
        case "tel":
          if (!e.value || e.value.length < 10) e.valid = false;
          break;
        default:
          break;
      }
    },
    focusHandler(e) {
      e.valid = true;
    },
    phoneMaskHandler(e) {
      if (e.code.indexOf("Key") === 0) {
        e.returnValue = false;
        if (e.preventDefault) e.preventDefault();
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.form-wrapper {
  margin: auto;

  .form-title {
    text-align: center;
    font-size: 20px;
    font-weight: 600;
    margin-bottom: 25px;
  }

  .attention {
    font-size: 12px;
    line-height: 125%;
    text-align: end;
    margin-bottom: 5px;
    opacity: 0.5;
  }

  .form {
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 20px;
    border: 1px solid #000;
    border-radius: 5px;
    box-shadow: 2px 2px 0 #000;
  }
}
</style>
