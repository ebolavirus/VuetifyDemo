<template>
  <v-container grid-list-xl>
    <v-layout wrap text-center>
      <v-expansion-panels v-model="panel" multiple>
        <v-expansion-panel>
          <v-expansion-panel-header>
            服务描述
            <template v-slot:actions>
              <v-icon color="primary">$vuetify.icons.expand</v-icon>
            </template>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-layout wrap>
              <v-flex xs4>
                <v-text-field label="*服务类型" append-outer-icon="mdi-file-document-box-search" readonly
                  @click:append-outer.stop="typeSelect" v-model="typeValue"></v-text-field>
                <v-dialog v-model="typedialog" persistent max-width="900px">
                  <v-card>
                    <v-card-title>
                      <span>变更类型选择列表</span>
                    </v-card-title>
                    <v-card-text>
                      <small>*特别提醒：正确地选择变更类型将大大加快流程处理速度，如果不清楚该选择何种变更，请致电0535-3388800。</small>
                      <v-container grid-list-md>
                        <v-layout wrap>
                          <v-flex xs12>
                            <v-data-table :headers="typeheaders" :items="typedesserts" :items-per-page="5"
                              class="elevation-1">
                              <template v-slot:item.action="{ item }">
                                <v-btn class="mb-2" @click="editItem(item)">选择</v-btn>
                              </template>
                            </v-data-table>
                          </v-flex>
                        </v-layout>
                      </v-container>
                    </v-card-text>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="typedialog = false">关闭</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </v-flex>
              <v-flex xs4>
                <v-radio-group v-model="row" row>
                  <template v-slot:label>
                    <div>*紧急程度：</div>
                  </template>
                  <v-radio label="普通" value="1"></v-radio>
                  <v-radio label="紧急" value="0"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs4>
                <v-text-field label="*办公室位置"></v-text-field>
              </v-flex>
              <v-flex xs12>
                <v-textarea label="服务内容"></v-textarea>
              </v-flex>
            </v-layout>
          </v-expansion-panel-content>
          <!-- IT顾问评估 -->
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-header>IT顾问评估</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-layout wrap>
              <v-flex xs12>
                <v-radio-group v-model="row" row xs6 sm3 md3>
                  <template v-slot:label>
                    <div>变更等级：</div>
                  </template>
                  <v-radio label="较小" value="0"></v-radio>
                  <v-radio label="中等" value="1"></v-radio>
                  <v-radio label="较大" value="2"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs4>
                <v-select :items="serviceTypes" label="服务分类" xs6 sm3 md3></v-select>
              </v-flex>
              <v-flex xs4>
                <v-text-field label="预估费用" suffix="元"></v-text-field>
              </v-flex>
              <v-flex xs4>
                <v-text-field label="预估实施" suffix="人天"></v-text-field>
              </v-flex>
              <v-flex xs6>
                <v-text-field label="办理人员名称" append-icon="mdi-anchor"></v-text-field>
              </v-flex>
              <v-flex xs6>
                <v-text-field label="通知人员" append-icon="mdi-anchor"></v-text-field>
              </v-flex>
              <v-flex xs12>
                <v-textarea label="评估意见"></v-textarea>
              </v-flex>
            </v-layout>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <!-- 办理人办理 -->
        <v-expansion-panel>
          <v-expansion-panel-header>办理人办理</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-layout wrap>
              <v-flex xs6>
                <v-text-field label="办理人员名称" append-icon="mdi-anchor"></v-text-field>
              </v-flex>
              <v-flex xs6>
                <v-text-field label="通知人员" append-icon="mdi-anchor"></v-text-field>
              </v-flex>
              <v-flex xs6>
                <v-text-field label="实际费用"></v-text-field>
              </v-flex>
              <v-flex xs6>
                <v-text-field label="实际实施"></v-text-field>
              </v-flex>
              <v-flex xs12>
                <v-textarea label="办理过程"></v-textarea>
              </v-flex>
              <v-flex xs12>
                <v-textarea label="原因分析"></v-textarea>
              </v-flex>
              <v-flex xs12>
                <v-textarea label="结果及建议"></v-textarea>
              </v-flex>
            </v-layout>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <!--  -->
        <v-expansion-panel>
          <v-expansion-panel-header>申请人验收</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-layout wrap>
              <v-flex xs6>
                <v-radio-group row>
                  <template v-slot:label>
                    <div>是否解决：</div>
                  </template>
                  <v-radio label="已解决" value="0"></v-radio>
                  <v-radio label="未解决" value="1"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs6>
                <v-radio-group row>
                  <template v-slot:label>
                    <div>是否满意：</div>
                  </template>
                  <v-radio label="满意" value="0"></v-radio>
                  <v-radio label="不满意" value="1"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs12>
                <v-textarea label="验收报告及建议"></v-textarea>
              </v-flex>
            </v-layout>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-header>
            附件
            <template v-slot:actions>
              <v-icon color="primary">$vuetify.icons.expand</v-icon>
            </template>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <iframe
              src="http://bpms.whchem.com/teamworks/fastExecuteServiceByName.jsp?processApp=EBCOMMA&serviceName=UI_Attachment&tw.local.instanceId=PIID-2d2bec22-f5d6-40e0-9eb9-b40a963d244e&tw.local.allowCreate=false&tw.local.allowUpdate=false&tw.local.allowDelete=false&tw.local.allowUpdateOthers=false&tw.local.allowDeleteOthers=false"
              style="width: 100%">
            </iframe>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      panel: [0, 1, 2, 3, 4, 5, 6],
      serviceTypes: ["type1", "type2", "type3", "type4", "type5"],
      typeValue: '',
      typedialog: false,
      typeheaders: [{
          text: '变更类型',
          align: 'left',
          sortable: false,
          value: 'name',
        },
        {
          text: '公司范围',
          value: 'calories'
        },
        {
          text: 'IT业务顾问',
          value: 'fat'
        },
        {
          text: '说明',
          value: 'carbs'
        },
        {
          text: '操作',
          value: 'action',
          sortable: false
        }
      ],
      typedesserts: [{
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: '1%',
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: '1%',
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: '7%',
        },
        {
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: '8%',
        },
        {
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: '16%',
        },
        {
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: '0%',
        },
        {
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: '2%',
        },
        {
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: '45%',
        },
        {
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: '22%',
        },
        {
          name: 'KitKat',
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: '6%',
        },
      ]
    }),
    methods: {
      typeSelect() {
        // let aaa = 1;
        // this.typeValue = aaa;
        this.typedialog = !this.typedialog;
      },
      editItem(aItem) {
        console.log('aaaaa', aItem);
      }
    }
  };
</script>