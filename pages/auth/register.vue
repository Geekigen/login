<template>
  <div>
    <!--
  Heads up! 👋

  Plugins:
    - @tailwindcss/forms
-->

    <section class="bg-white">
      <div class="lg:grid lg:min-h-screen lg:grid-cols-12">
        <aside class="relative block h-16 lg:order-last lg:col-span-5 lg:h-full xl:col-span-6">
          <img alt=""
            src="https://images.unsplash.com/photo-1605106702734-205df224ecce?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80"
            class="absolute inset-0 h-full w-full object-cover" />
        </aside>

        <main class="flex items-center justify-center px-8 py-8 sm:px-12 lg:col-span-7 lg:px-16 lg:py-12 xl:col-span-6">
          <div class="max-w-xl lg:max-w-3xl">

            <h1 class="mt-6 text-2xl font-bold text-gray-900 sm:text-3xl md:text-4xl">
              Welcome to Spin 🦑
            </h1>

            <p class="mt-4 leading-relaxed text-gray-500">
              Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eligendi nam dolorum aliquam,
              quibusdam aperiam voluptatum.
            </p>

            <form action="#" class="mt-8 grid grid-cols-6 gap-6">
              <div class="col-span-6 sm:col-span-3">
                <label for="FirstName" class="block text-sm font-medium text-gray-700">
                  First Name
                </label>

                <input type="text" id="FirstName" name="first_name"
                v-model="form.username"
                  class="mt-1 w-full rounded-md border-gray-200 bg-white text-sm text-gray-700 shadow-sm" />
              </div>

            

              <div class="col-span-6">
                <label for="Email" class="block text-sm font-medium text-gray-700"> Email </label>

                <input type="email" id="Email" name="email"
                v-model="form.email"
                  class="mt-1 w-full rounded-md border-gray-200 bg-white text-sm text-gray-700 shadow-sm" />
              </div>

              <div class="col-span-6 sm:col-span-3">
                <label for="Password" class="block text-sm font-medium text-gray-700"> Password </label>

                <input type="password" id="Password" name="password"
                v-model="form.password1"
                  class="mt-1 w-full rounded-md border-gray-200 bg-white text-sm text-gray-700 shadow-sm" />
              </div>

              <div class="col-span-6 sm:col-span-3">
                
                <label for="PasswordConfirmation" class="block text-sm font-medium text-gray-700">
                  Password Confirmation
                </label>

                <input type="password" id="PasswordConfirmation" name="password_confirmation"
                v-model="form.password2"
                  class="mt-1 w-full rounded-md border-gray-200 bg-white text-sm text-gray-700 shadow-sm" />
              </div>

              <div class="col-span-6 sm:col-span-3">
                
                <label for="role" class="block text-sm font-medium text-gray-700">
                  Role
                </label>
                <select id="role" name="role"  v-model="form.role"
                  class="mt-1 w-full rounded-md border-gray-200 bg-white text-sm text-gray-700 shadow-sm">
              <option value=""></option>

                </select>
                
               </div>

              

              <div class="col-span-6 sm:flex sm:items-center sm:gap-4">
                <button 
                type="button"
                @click="handlesubmit"
                  class="inline-block shrink-0 rounded-md border border-blue-600 bg-blue-600 px-12 py-3 text-sm font-medium text-white transition hover:bg-transparent hover:text-blue-600 focus:outline-none focus:ring active:text-blue-500">
                  Create an account
                </button>

                <p class="mt-4 text-sm text-gray-500 sm:mt-0">
                  Already have an account?
                  <a href="/auth/login" class="text-gray-700 underline">Log in</a>.
                </p>
              </div>
            </form>
          </div>
        </main>
      </div>
    </section>
  </div>
</template>

<script>

export default {
  name: 'Register',
  data() {
    return {
      error: '',
      form: {
        username: '',
        email: '',
        firstName: '',
        lastName: '',
        password1: '',
        password2: '',
        role: ''
      }
    }
  },
  methods: {
    async handlesubmit() {
      try {
        const response = await $fetch('http://127.0.0.1:8000/api/register/', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: {
            username: this.form.username,
            email: this.form.email,
            password1: this.form.password1,
            password2: this.form.password2,
            user_role: this.form.role
          }

        });
        if(response.code !== "201")
        alert(response.message)
        else
         return await navigateTo('/auth/Confirmation')
      }
//       async  getRole(){
//         try{
// const response = $fetch()

//         }
//       }
     
      catch (error) {
        console.error('An error occurred:', error);

      }
    }

  }
}
</script>