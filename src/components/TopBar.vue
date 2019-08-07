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
    <v-btn text @click="saveAction()">
      <span class="mr-2">保存</span>
    </v-btn>
    <v-btn text @click="rejectAction()">
      <span class="mr-2">驳回</span>
    </v-btn>
    <v-btn text @click="cancelAction()">
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
    <v-btn text @click="progressGraphAction()">
      <span class="mr-2">流程图</span>
    </v-btn>
    <v-btn text>
      <span class="mr-2">关闭</span>
    </v-btn>
    <!-- 提交对话框 -->
    <v-dialog v-model="dialog2" max-width="800px">
      <v-card>
        <v-card-title>审批人</v-card-title>
        <v-card-text>
          <v-layout wrap>
            <v-flex xs12>
              <v-textarea label="审批意见" counter="300" value="同意" clearable></v-textarea>
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
    <!-- 流程图对话框 http://bpmqas02.whchem.com/ECS_BPM_ADV/jsp/trdpty/processMapNew.jsp?bpdId=25.3e223090-6578-4686-98da-1ab9b0d1feff&appShortName=ITAPP&tsPiid=PIID-6a769121-f3cc-4dff-9cd7-4b9e1ff1bf62&snapshotId=2064.25fda463-fbb1-448d-ae01-c0791db69ea1 -->
    <v-dialog v-model="dialog3" max-width="1000px">
      <v-card>
        <v-card-title>流程图</v-card-title>
        <v-card-text>
          <v-layout align-center justify-center>
            <v-img
              src="../assets/25.jpg"
              aspect-ratio="1"
              class="grey lighten-2"
              max-width="1000"
              max-height="680"
              contain
            ></v-img>
          </v-layout>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" text @click="dialog3 = false">关闭</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <!-- 保存业务数据 -->
    <v-alert dismissible elevation="2" v-if="saved" type="info">保存业务数据成功!</v-alert>
    <!-- 驳回对话框 -->
    <v-dialog v-model="dialog5" max-width="800px">
      <v-card>
        <v-card-title>任务驳回</v-card-title>
        <v-card-text>
          <v-layout wrap>
            <v-flex xs12 sm6>
              <v-select :items="['起草@Draft']" label="驳回到环节" required></v-select>
            </v-flex>
            <v-flex xs12>
              <v-textarea label="审批意见" counter="300" value="同意" clearable required></v-textarea>
            </v-flex>
          </v-layout>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" text @click="dialog5 = false">关闭</v-btn>
          <v-btn color="primary" text @click="dialog5 = false">驳回</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <!-- 注销流程 -->
    <v-dialog v-model="dialog4" max-width="300px">
      <v-card>
        <v-card-title>注销流程</v-card-title>
        <v-card-text>您确定要注销当前单据吗？</v-card-text>
        <v-card-actions>
          <v-btn color="primary" text @click="dialog4 = false">关闭</v-btn>
          <v-btn color="primary" text @click="dialog4 = false">注销</v-btn>
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
    dialog3: false,
    // 注销对话框开关
    dialog4: false,
    // 驳回对话框开关
    dialog5: false,
    saved: false,
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
      this.dialog2 = true;
    },
    progressGraphAction() {
      this.dialog3 = true;
    },
    saveAction() {
      console.log("saveAction");
      this.saved = true;
    },
    cancelAction() {
      this.dialog4 = true;
    },
    rejectAction() {
      this.dialog5 = true;
    }
  }
};
</script>
