<template>
  <div class="login">
      <h2>Login</h2>
      <form @submit.prevent="login">
          <input type="email" v-model="email" placeholder="Email" required />
          <input type="password" v-model="password" placeholder="Password" required />
          <button type="submit">Login</button>
      </form>
      <p v-if="error" class="error">{{ error }}</p>

  </div>
</template>

<script>
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import { ref, onMounted } from 'vue'


export default {
  setup() {
      const store = useStore();
      const router = useRouter();
      const email = ref('');
      const password = ref('');

      const login = async () => {
          try {
              await store.dispatch('login', { email: email.value, password: password.value });
              router.push('/dashboard');
          } catch (error) {
              console.error('Error logging in: ', error);
          }
      };

      return {
          email,
          password,
          login
      };
  }

};
</script>

<style>
.error {
  color: red;
  margin-top: 10px;
}
</style>