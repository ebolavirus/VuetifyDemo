<template>
  <v-app-bar color="primary" app dark>
    <v-btn @click="drawerAction()" icon>
      <v-app-bar-nav-icon />
    </v-btn>
    <v-toolbar-title class="headline text-uppercase">
      <span class="mr-2">Vuetify信息服务申请DEMO</span>
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn text @click="submitAction()">
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
          <span class="mr-2">高级▾</span>
        </v-btn>
      </template>
      <v-list>
        <v-list-item v-for="(item, index) in baritems" :key="index">
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
    <v-dialog v-model="dialog2" max-width="800px">
      <v-card>
        <v-card-title>审批人</v-card-title>
        <v-card-text>
          <v-layout wrap>
            <v-flex xs12>
              <v-textarea label="审批意见">同意</v-textarea>
            </v-flex>
            <v-flex xs6>
              <v-text-field label="下一任务" value="IT顾问评估"></v-text-field>
            </v-flex>
            <v-flex xs6>
              <v-text-field label="任务类型" value="单一签核"></v-text-field>
            </v-flex>
            <v-flex xs12>
              <v-data-table
                :headers="apHeaders"
                :items="approvers"
                :items-per-page="5"
                class="elevation-1"
                single-select
                v-model="selectedApprover"
                item-key="name"
                show-select
              ></v-data-table>
            </v-flex>
          </v-layout>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" text @click="dialog2 = false">关闭</v-btn>
          <v-btn color="primary" text @click="dialog2 = false">提交</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app-bar>
</template>

<script>
export default {
  model: {
    prop: "drawerprop",
    event: "itemChanged"
  },
  props: {
    drawerprop: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    drawer: {
      get() {
        return this.drawerprop;
      },
      set(value) {
        this.$emit("itemChanged", value);
      }
    }
  },
  data: () => ({
    baritems: [
      { title: "加签", icon: "dashboard" },
      { title: "转办", icon: "account_box" },
      { title: "通知", icon: "gavel" }
    ],
    dialog2: false,
    apHeaders: [
      {
        text: "名称",
        align: "left",
        sortable: false,
        value: "name"
      },
      { text: "部门", value: "dept" }
    ],
    approvers: [
      {
        name: "何凭",
        dept: "/万华集团/万华化学/信息中心/基础设施"
      },
      {
        name: "王海洋",
        dept: "/万华集团/万华化学/信息中心/基础设施"
      }
    ],
    selectedApprover: []
  }),
  methods: {
    drawerAction() {
      this.$emit("drawerclick");
    },
    submitAction() {
      // console.log("submit");
      this.dialog2 = true;
    }
  }
};
</script>
