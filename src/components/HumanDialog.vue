<template>
  <v-dialog v-model="intypedialog" fullscreen hide-overlay>
    <!-- transition="dialog-bottom-transition"> -->
    <v-card>
      <v-toolbar dark color="primary">
        <v-btn icon dark @click="intypedialog = false">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-toolbar-title>选择人员</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items>
          <v-btn dark text @click="editItem">确认</v-btn>
        </v-toolbar-items>
      </v-toolbar>
      <v-container grid-list-md>
        <v-layout wrap>
          <v-flex sm3 order-sm1 v-if="$vuetify.breakpoint.smAndUp">
            <v-card>
              <v-card-text>
                <v-text-field label="搜索部门" append-outer-icon="mdi-file-document-box-search" value="信息中心" readonly>
                </v-text-field>
                <v-treeview selectable selected-color="amber" :items="departmentitems"></v-treeview>
              </v-card-text>
            </v-card>
          </v-flex>
          <v-flex xs12 sm6 order-xs2 order-sm2>
            <v-card>
              <v-card-text>
                <v-text-field label="搜索人员" placeholder="ITCODE,中文名，英文名等"
                  append-outer-icon="mdi-file-document-box-search" value="mmsuna"></v-text-field>
                <v-data-table :headers="typeheaders" :items="typedesserts" :items-per-page="5" show-select
                  item-key="name" v-model="listSelectValue" class="elevation-1">
                </v-data-table>
              </v-card-text>
            </v-card>
          </v-flex>
          <v-flex xs12 sm3 order-xs1 order-sm3>
            <v-card>
              <v-card-title>选中人员列表</v-card-title>
              <v-card-text>
                <v-data-table dense :headers="typeheaders2" :items="listSelectValue" :items-per-page="1000" show-select
                  item-key="name" hide-default-header hide-default-footer no-data-text="没有人员选中" height="300"
                  v-model="listSelectValue2" class="elevation-1">
                </v-data-table>
                <div class="text-center pt-2">
                  <v-btn color="primary" class="mr-2" @click="removeItem(0)">移除选中</v-btn>
                  <v-btn color="primary" @click="removeItem(1)">移除全部</v-btn>
                </div>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    model: {
      prop: "typedialog",
      event: "dialogChanged"
    },
    props: {
      typedialog: {
        type: Boolean,
        default: false
      }
    },
    data: () => ({
      typeheaders: [{
          text: "ID",
          align: "left",
          value: "name"
        },
        {
          text: "姓名",
          value: "calories"
        },
        {
          text: "部门",
          value: "fat"
        },
        {
          text: "工号",
          value: "carbs"
        }
      ],
      typeheaders2: [{
        text: "姓名",
        value: "calories"
      }],
      typedesserts: [{
          name: "zmmo",
          calories: '莫泽梦',
          fat: '水性装置',
          carbs: '00003246',
        },
        {
          name: "jmmao",
          calories: '毛建明',
          fat: '设备部电气运行',
          carbs: '00000384',
        },
        {
          name: "mmyang",
          calories: '杨萌萌',
          fat: '电气管理',
          carbs: '00003009'
        },
        {
          name: "mmgao",
          calories: '高明明',
          fat: '土建管理',
          carbs: '00003597'
        },
        {
          name: "mmhe",
          calories: '何明明',
          fat: '环氧丙烷装置大横班丁班',
          carbs: '00003713'
        },
        {
          name: "mmhe",
          calories: '何明明',
          fat: '环氧丙烷装置大横班丁班',
          carbs: '00003713'
        }, {
          name: "zmmo",
          calories: '莫泽梦',
          fat: '水性装置',
          carbs: '00003246',
        },
        {
          name: "jmmao",
          calories: '毛建明',
          fat: '设备部电气运行',
          carbs: '00000384',
        },
        {
          name: "mmyang",
          calories: '杨萌萌',
          fat: '电气管理',
          carbs: '00003009'
        },
        {
          name: "mmgao",
          calories: '高明明',
          fat: '土建管理',
          carbs: '00003597'
        }
      ],
      departmentitems: [{
          id: 1,
          name: "万华化学集团股份有限公司",
          children: [{
              id: 2,
              name: "信息中心",
              children: [{
                  id: 26,
                  name: "协同办公"
                },
                {
                  id: 27,
                  name: "财务IT"
                },
                {
                  id: 28,
                  name: "基础设施"
                }
              ]
            },
            {
              id: 3,
              name: "工业园"
            },
            {
              id: 4,
              name: "市场部"
            }
          ]
        },
        {
          id: 5,
          name: "万华实业集团股份有限公司",
          children: [{
              id: 6,
              name: "财务部",
              children: [{
                id: 7,
                name: "资产管理部",
                children: [{
                  id: 8,
                  name: "销售部"
                }, {
                  id: 9,
                  name: "典当部"
                }]
              }]
            },
            {
              id: 10,
              name: "总裁办公室",
              children: [{
                id: 11,
                name: "总裁办",
                children: [{
                    id: 12,
                    name: "办公室1"
                  },
                  {
                    id: 13,
                    name: "办公室2"
                  },
                  {
                    id: 14,
                    name: "办公室3"
                  }
                ]
              }]
            }
          ]
        },
        {
          id: 15,
          name: "万华板业",
          children: [{
              id: 16,
              name: "研究院"
            },
            {
              id: 17,
              name: "财务部"
            },
            {
              id: 18,
              name: "审计部"
            }
          ]
        },
        {
          id: 19,
          name: "烟台码头",
          children: [{
              id: 20,
              name: "综合部",
              children: [{
                  id: 21,
                  name: "财务部"
                },
                {
                  id: 22,
                  name: "HSE部"
                },
                {
                  id: 23,
                  name: "生产部"
                }
              ]
            },
            {
              id: 24,
              name: "经营部"
            },
            {
              id: 25,
              name: "工程技术部"
            }
          ]
        }
      ],
      notifications: false,
      sound: true,
      widgets: false,
      listSelectValue: [],
      listSelectValue2: []
    }),
    watch: {
      listSelectValue(to, from) {
        console.log('changed:::', to, from);
      }
    },
    computed: {
      intypedialog: {
        get() {
          return this.typedialog;
        },
        set(value) {
          this.$emit("dialogChanged", value);
        }
      }
    },
    methods: {
      editItem() {
        let valueresult = '';
        for (let i in this.listSelectValue) {
          console.log(i);
          valueresult += this.listSelectValue[i].calories;
          valueresult += ','
        }
        this.$emit("dialogSelected", valueresult);
        this.intypedialog = false;
      },
      removeItem(key, value) {
        console.log(key, value);
        console.log(this.$vuetify.breakpoint.width);
        this.listSelectValue = [];
      }
    }
  };
</script>