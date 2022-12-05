<template>
    <main class="main">
        <div v-if="!isSend" class="form-wrapper">
            <div class="form-title">
                Форма регистрации
            </div>
            <div class="attention">* обязательное поле</div>
            <form action="" class="form">
                <input type="text" name="name" placeholder="Имя*" v-model="form.name" required />
                <input type="text" name="surname" placeholder="Фамилия*" v-model="form.surname" required />
                <input type="email" name="email" placeholder="Email*" v-model="form.email" required />
                <input type="tel" name="phone" placeholder="Телефон*" v-model="form.phone" required />
                <input type="date" name="birthday" placeholder="Дата рождения" v-model="form.birthday" />
                <select name="gender" v-model="form.gender">
                    <option value="" selected disabled>Пол</option>
                    <option value="male">Мужской</option>
                    <option value="female">Женский</option>
                </select>
                <label for="privacy" class="privacy-label">
                    <input type="checkbox" name="privacy" id="privacy" v-model="form.privacy" required>
                    *Согласен с ...
                </label>
                <button :disabled="!validForm" @click.prevent="sendFormHandler">Отправить</button>
            </form>
        </div>
        <div v-else class="form-wrapper">
            <div class="form">
                <div class="form-title">
                    Форма успешно оправлена!
                </div>
            </div>
        </div>
    </main>
</template>
<style lang="scss" src="./app.scss">

</style>
<script>
export default {
    name: 'App',
    data() {
        return {
            form: {
                name: '',
                surname: '',
                phone: '',
                email: '',
                birthday: '',
                gender: '',
                privacy: false
            },
            isSend: false
        }
    },
    computed: {
        validForm() {
            let valid = true;

            if (!this.form.name || this.form.name.length < 2) valid = false;
            if (!this.form.surname || this.form.surname.length < 2) valid = false;
            if (!this.form.email || this.form.email.length < 6) valid = false;
            if (!this.form.phone || this.form.phone.length < 10) valid = false;
            if (!this.form.privacy) valid = false;

            return valid;
        }
    },
    methods: {
        sendFormHandler() {
            this.isSend = true;
        }
    }
};
</script>