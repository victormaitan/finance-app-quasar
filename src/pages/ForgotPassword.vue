<template>
  <q-page class="flex flex-center bg-dark">

     <q-card style="width: 300px; height: 250px">
      <q-card-section class="q-mt-md">
        <div class="text-h5">Forgot password?</div>
      </q-card-section>

      <q-card-section class="q-pt-lg">
        <q-input class="q-mb-sm" rounded outlined v-model="user.email" label="Email" />
      </q-card-section>

      <q-card-actions>
        <q-btn color="primary" outline label="Back" style="width: 48%" @click="$router.push({ name: 'login' })"/>
        <q-btn color="primary" label="Reset password" style="width: 48%" @click="$router.push({ name: 'login' })"/>
      </q-card-actions>
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
