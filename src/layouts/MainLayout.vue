<template>
  <q-layout view="lHh Lpr lFf">
	<q-header
    elevated
  >
    <div class="container">
        <q-toolbar>
          <div style="display:flex; justify-content:space-between; width:100%">
            <div style="width:300px">
              <q-input color="grey" outlined v-model="text" label="Поиск" :dense="true">
                <template v-slot:append>
                  <q-icon name="search" />
                </template>
              </q-input>
            </div>
            <div>
              <q-btn icon="add" label="Создать отель" color="primary" />
            </div>
          </div>
      </q-toolbar>
    </div>
	</q-header>

	<q-drawer
	  v-model="leftDrawerOpen"
	  show-if-above
	  bordered
	>
	  <q-list>
      <q-item-label
        header
        bordered
      >
        <router-link to="/">
          <img src="../assets/logo.png">
        </router-link>
      </q-item-label>

      <EssentialLink
        v-for="link in essentialLinks"
        :key="link.title"
        v-bind="link"
      />
	  </q-list>
	</q-drawer>
	<q-page-container>
	  <router-view />
	</q-page-container>
  </q-layout>
</template>
<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
	title: 'Дашборд',
	caption: 'quasar.dev',
	icon: 'svguse:icons.svg#dashboard_admin',
	link: 'https://quasar.dev'
  },
  {
	title: 'Отели',
	caption: 'github.com/quasarframework',
	icon: 'svguse:icons.svg#hotel_admin',
	link: 'https://github.com/quasarframework'
  },
  {
	title: 'История событий',
	caption: 'chat.quasar.dev',
	icon: 'svguse:icons.svg#history_admin',
	link: 'https://chat.quasar.dev'
  },
  {
	title: 'Профиль',
	caption: 'forum.quasar.dev',
	icon: 'svguse:icons.svg#account_admin',
	link: 'https://forum.quasar.dev'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
	EssentialLink
  },

  setup () {
	const leftDrawerOpen = ref(false)

	return {
	  essentialLinks: linksList,
	  leftDrawerOpen,
	  toggleLeftDrawer () {
		leftDrawerOpen.value = !leftDrawerOpen.value
	  }
	}
  }
})
</script>

<style lang="scss">
.q-list{
  .q-item{
    svg{
      fill-opacity: 0.54;
      fill:black;
    }
  }
}
</style>
