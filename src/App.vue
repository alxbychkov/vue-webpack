<template>
  <main class="main">
    <Form
      v-if="!isSend"
      title="Форма регистрации"
      attention="* обязательное поле"
      name="register"
      @onSubmit="submitFormHandler"
    />
    <div v-else class="message-wrapper">
      <div class="message-title">{{ name }}, форма успешно оправлена!</div>
    </div>
  </main>
</template>

<script>
import Form from "./components/form/Form.vue";
import { capitalizeFirstLetter } from "./helpers/functions.js";

export default {
  name: "App",
  components: { Form },
  data() {
    return {
      isSend: false,
      name: null,
    };
  },
  methods: {
    async submitFormHandler(form) {
      this.name = capitalizeFirstLetter(form.name);
      // Send data
      // await fetch('/form.php', form);
      // if response ok show message
      this.isSend = form.valid;
    },
  },
};
</script>
