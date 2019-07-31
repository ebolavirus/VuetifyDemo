<template>
    <v-navigation-drawer
      app
      v-model="drawer"
      dark
    >
      <v-list>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link>
          <!-- <v-list-item-icon>
            <v-icon>{{item.icon}}</v-icon>
          </v-list-item-icon> -->
          <v-list-item-content>
            <v-list-item-title>{{item.title}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
</template>

<script>
export default {
  model: {
    prop: 'drawerprop',
    event: 'itemChanged'
  },
  props: {
    drawerprop: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    drawer: {
      get () {
        return this.drawerprop
      },
      set (value) {
        this.$emit('itemChanged', value);
      }
    }
  },
  data: () => ({
    items: [
      {title: 'Dashboard', icon: 'dashboard'},
      {title: 'Account', icon: 'account_box'},
      {title: 'Admin', icon: 'gavel'}
    ]
  })
};
</script>
