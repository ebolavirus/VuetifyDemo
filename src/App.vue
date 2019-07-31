<template>
  <v-app>
    <Sidedrawer
      v-model="draweropen"
    />
    <v-app-bar app>
      <v-btn
        @click="draweropen = !draweropen"
        icon>
        <v-app-bar-nav-icon />
      </v-btn>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify版</span>
        <span class="font-weight-light">信息服务申请DEMO</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        text
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Sidedrawer from './components/Sidedrawer';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Sidedrawer
  },
  data: () => ({
    draweropen: true
  }),
};
</script>
