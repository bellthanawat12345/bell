<template>
    <div class="login">
      
  <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto  lg:py-0">

      <div class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
          <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
              <h1 class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
                  ลงชื่อเข้าใช้งาน
              </h1>
              <form class="space-y-4 md:space-y-6"  @submit.prevent="login">
                  <div>
                      <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Email</label>
                      <input type="email" name="email" v-model="email"  id="email" class="bg-gray-50 border border-gray-300 text-gray-900 rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="name@company.com" required="">
                  </div>
                  <div>
                      <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
                      <input type="password" name="password"  v-model="password" id="password" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required="">
                  </div>
                  <div class="flex items-center justify-between">
                      <div class="flex items-start">
                          <div class="flex items-center h-5">
                            <input id="remember" aria-describedby="remember" type="checkbox" class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-primary-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-primary-600 dark:ring-offset-gray-800" required="">
                          </div>
                        <div class="ml-3 text-sm">
                            <label for="remember" class="text-gray-500 dark:text-gray-300">Remember me</label>
                          </div>
                      </div>
               
                  </div>
                   <div>
        <button type="submit" class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Sign in</button>
      </div>
              </form>
              <p v-if="error" class="error">{{ error }}</p>
          </div>
      </div>
  </div>


        

    </div>
</template>

<script >
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