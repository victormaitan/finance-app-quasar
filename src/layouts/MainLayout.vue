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

        <q-toolbar-title>
          Finance App
        </q-toolbar-title>

        <q-btn flat class="" icon-right="exit_to_app" color="white" label="Logout" @click="$router.push({ name: 'login' })"/>

      </q-toolbar>
    </q-header>

    <q-drawer
      dark
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Menu
        </q-item-label>
        <q-item
          clickable
          tag="a"
          target="_blank"
          href=""
        >
          <q-item-section
            v-if="icon"
            avatar
          >
            <q-icon name="person" />
          </q-item-section>

          <q-item-section>
            <q-item-label> Titulo</q-item-label>
            <q-item-label caption>
              Descrição
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
