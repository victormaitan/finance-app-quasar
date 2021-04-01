<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title class="row justify-center">
          <q-img
            src="https://raw.githubusercontent.com/rocketseat-education/maratona-discover-01/9d0b7435ded694abeba1e932c1f9b3f263fecbff/assets/logo.svg"
            spinner-color="white"
            style="height: 20px; width: 150px"
          />
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer dark v-model="leftDrawerOpen" bordered content-class="bg-grey-1">
      <q-list>
        <q-item-label header class="text-grey-8">
          Menu
        </q-item-label>
        <q-item clickable @click="$router.push({ name: 'login' })">
          <q-item-section avatar class="text-black row">
            <q-item-label>
              Sair do App
              <q-icon name="exit_to_app" color="black" size="xs"/>
            </q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view/>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false
    }
  }
}
</script>
