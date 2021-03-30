<template>
  <q-page class="flex flex-center bg-dark">

     <q-card style="width: 300px; height: 400px">
      <q-card-section class="row justify-center q-mt-md">
        <div class="text-h4">LOGIN</div>
      </q-card-section>

      <q-card-section class="q-pt-lg">
        <q-input class="q-mb-sm" rounded outlined v-model="user.email" label="Email" />
        <q-input label="Password" v-model="user.password" rounded outlined :type="user.isPwd ? 'password' : 'text'">
          <template v-slot:append>
            <q-icon
              :name="user.isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="user.isPwd = !user.isPwd"
            />
          </template>
        </q-input>
      </q-card-section>

      <q-card-section class="row q-pt-xl">
        <q-btn class="full-width q-mb-sm" color="primary" label="Login" @click="$router.push({ name: 'home' })"/>
        <q-btn class="full-width" flat color="primary" no-caps label="Forgot Password" @click="$router.push({ name: 'forgot' })"/>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      user: {
        email: '',
        password: '',
        isPwd: !false
      }
    }
  }
}
</script>
