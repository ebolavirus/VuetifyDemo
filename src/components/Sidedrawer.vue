<template>
  <v-navigation-drawer app v-model="drawer" dark width="400">
    <v-expansion-panels v-model="panel" :accordion="true" :multiple="true">
      <v-expansion-panel>
        <v-expansion-panel-header>
          基本信息
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-data-table hide-default-header hide-default-footer :headers="headers" :items="desserts"
            class="elevation-1"></v-data-table>
        </v-expansion-panel-content>
      </v-expansion-panel>
      <v-expansion-panel>
        <v-expansion-panel-header>
          审批历史
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-timeline dense>
            <v-timeline-item color="amber lighten-1" fill-dot right small>
              <v-card>
                <v-card-title class="amber">
                  <span class="white--text">当前环节</span>
                </v-card-title>
                <v-container>
                  <v-layout>
                    <v-flex>
                      孙明明(mmsuna)<br>单一签核
                    </v-flex>
                  </v-layout>
                </v-container>
              </v-card>
            </v-timeline-item>
            <v-timeline-item color="green lighten-1" fill-dot right>
              <v-card>
                <v-card-title class="green lighten-1">
                  <span class="white--text">起草-提交</span>
                </v-card-title>
                <v-container>
                  <v-layout>
                    <v-flex>
                      孙明明(mmsuna)<br>2019-7-19 10:36:26<br>用时0天<br>同意
                    </v-flex>
                  </v-layout>
                </v-container>
              </v-card>
            </v-timeline-item>
            <v-timeline-item color="green lighten-1" fill-dot right>
              <v-card>
                <v-card-title class="green lighten-1">
                  <span class="white--text">起草-提交</span>
                </v-card-title>
                <v-container>
                  <v-layout>
                    <v-flex>
                      孙明明(mmsuna)<br>2019-7-19 10:36:26<br>用时0天<br>同意
                    </v-flex>
                  </v-layout>
                </v-container>
              </v-card>
            </v-timeline-item>
          </v-timeline>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
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
        get() {
          return this.drawerprop
        },
        set(value) {
          this.$emit('itemChanged', value);
        }
      }
    },
    data: () => ({
      panel: [0, 1],
      items: [{
          title: 'Dashboard',
          icon: 'dashboard'
        },
        {
          title: 'Account',
          icon: 'account_box'
        },
        {
          title: 'Admin',
          icon: 'gavel'
        }
      ],
      headers: [{
          text: '',
          align: 'left',
          sortable: false,
          value: 'name',
        },
        {
          text: '',
          value: 'calories'
        }
      ],
      desserts: [{
          name: '申请单号',
          calories: 'IT20190700909'
        },
        {
          name: '申请日期',
          calories: '2019-7-19 10:36:26'
        },
        {
          name: '申请人',
          calories: '孙明明（mmsuna）'
        },
        {
          name: '联系方式',
          calories: '18153517065'
        },
        {
          name: '所属组织',
          calories: '/万华集团/万华化学集团股份有限公司/信息中心/协同办公'
        }
      ]
    })
  };
</script>