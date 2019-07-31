<template>
    <v-app-bar
      color="primary"
      app
      dark>
      <v-btn
        @click="drawerAction()"
        icon>
        <v-app-bar-nav-icon />
      </v-btn>
      <v-toolbar-title class="headline text-uppercase">
        <span class="mr-2">Vuetify信息服务申请DEMO</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text>
        <span class="mr-2">提交</span>
      </v-btn>
      <v-btn text>
        <span class="mr-2">保存</span>
      </v-btn>
      <v-btn text>
        <span class="mr-2">注销</span>
      </v-btn>
      <v-menu offset-y>
        <template v-slot:activator="{on}">
          <v-btn text v-on="on">
            <span class="mr-2">高级▽</span>
          </v-btn>
        </template>
        <v-list>
          <v-list-item
            v-for="(item, index) in baritems"
            :key="index"
          >
            <v-list-item-title>{{item.title}}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <v-btn text>
        <span class="mr-2">帮助</span>
      </v-btn>
      <v-btn text>
        <span class="mr-2">流程图</span>
      </v-btn>
      <v-btn text>
        <span class="mr-2">关闭</span>
      </v-btn>
    </v-app-bar>
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
    baritems: [
      {title: '加签', icon: 'dashboard'},
      {title: '转办', icon: 'account_box'},
      {title: '通知', icon: 'gavel'}
    ]
  }),
  methods: {
    drawerAction () {
      this.$emit('drawerclick');
    }
  }
};
</script>
