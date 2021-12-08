<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <HelloWorld></HelloWorld>
    </v-navigation-drawer>
    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Application</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn color="secondary">Secondary</v-btn>
      <v-btn @click="toggleDark">toggle theme</v-btn>
    </v-app-bar>
    <v-main>
      <!-- <div>ZCalendar</div> -->
      <ZCalendar :gutters="false"></ZCalendar>
    </v-main>
  </v-app>
</template>

<script>
import { ref } from '@vue/composition-api'
import ZCalendar from './components/ZCalendar.vue'
import HelloWorld from './components/HelloWorld.vue'

export default {
  setup(props, context) {
    const collapsed = ref(false);
    const drawer = ref(false);
    const toggleDark = () => {
      // eslint-disable-next-line no-debugger
      // debugger
      context.root.$vuetify.theme.dark = !context.root.$vuetify.theme.dark;
    }

    return {
      collapsed,
      drawer,
      toggleDark
    };
  },
  components: { ZCalendar, HelloWorld },
  methods: {
    setTheme() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    }
  }
}
</script>
