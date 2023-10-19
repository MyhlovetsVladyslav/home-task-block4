<template>
  <div :class="{ 'dark-theme': isDark }">
    <p>Шосте завдання</p>
    <button @click="toggleTheme">Переключить тему</button>
    <time-component></time-component>
    <p>Друге завдання</p>
    <form @submit.prevent="submitForm">
      <label for="name">Ім'я:</label>
      <input type="text" id="name" v-model="name" required>
      <span v-show="errors.messageName" class="error">{{ errors.messageName }}</span>
      <br>
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="email" required>
      <span v-show="errors.messageEmail" class="error">{{ errors.messageEmail }}</span>
      <br>
      <button type="submit">Відправити</button>
    </form>
    <hr>
    <p>Перевірка на авторизацію| Третє завдання</p>
    <button @click="handleSubmit">Перевірить</button>
    <hr>
    <table-component></table-component>
    <list-objects></list-objects>
  </div>
</template>

<script>
import timeComponent from './components/timeComponent.vue';
import tableComponent from './components/tableComponent.vue';
import listObjects from './components/listObjects.vue';
export default {
  name: 'App',
  data() {
    return {
      name: '',
      email: '',
      isLoged: false,
      errors: {
        messageEmail: '',
        messageName: ''
      },
      isDark: false
    }
  },
  components: {
    timeComponent,
    tableComponent,
    listObjects
  },
  methods: {
    toggleTheme() {
      this.isDark = !this.isDark;
    },

    submitForm() {
      this.errors = {
        messageName: this.name.length < 4 ? 'Введіть коректне значення' : '',
        messageEmail: this.validateEmail(this.email) ? '' : 'Введіть коректне значення'
      }
      if (this.errors.messageName === '' && this.errors.messageEmail === '') {
        console.log('Дані були успішно відправлені:', this.name, this.email);
        this.isLoged = true
      }
    },
    validateEmail(email) {
      const symbol = /^\S{5,}@\S+\.\S+$/;
      return symbol.test(email);
    },
    sendMessageRegister() {
      console.log("Ви не зареєстровані");
    },
    sendMessageAutoris() {
      console.log("Ви зареєстровані");
    },
    handleSubmit() {
      if (this.isLoged === true) {
        this.sendMessageAutoris()
      } else if (this.isLoged === false) {
        this.sendMessageRegister()
      }
    }

  },
}
</script>

<style scoped>
.dark-theme {
  background-color: #333;
  color: #fff;
}
</style>
