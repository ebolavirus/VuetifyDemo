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
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="*服务类型" append-outer-icon="mdi-file-document-box-search" readonly
                  @click:append-outer.stop="typeSelect" v-model="typeValue"></v-text-field>
                <TypeDialog v-model="typedialog" @dialogSelected="typeDialogSelected" />
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <WanhuaRadio />
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="*办公室位置"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <TextfieldReadonly titleValue="办公室位置（只读）" realValue="信息中心十五楼八层" />
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
              <v-flex xs12 sm6 md6 lg6>
                <v-radio-group v-model="row" row xs6 sm3 md3>
                  <template v-slot:label>
                    <div>变更等级：</div>
                  </template>
                  <v-radio label="较小" value="0"></v-radio>
                  <v-radio label="中等" value="1"></v-radio>
                  <v-radio label="较大" value="2"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-select :items="serviceTypes" label="服务分类"></v-select>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="预估费用" type="number" suffix="元"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="实施日期" type="date"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="办理人员名称" append-outer-icon="mdi-file-document-box-search" readonly
                  @click:append-outer.stop="dutySelect" v-model="dutyValue"></v-text-field>
                <HumanDialog v-model="dutydialog" @dialogSelected="dutyDialogSelected" />
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="通知人员" append-outer-icon="mdi-file-document-box-search" readonly
                  @click:append-outer.stop="dutySelect" v-model="dutyValue"></v-text-field>
                <HumanDialog v-model="dutydialog" @dialogSelected="dutyDialogSelected" />
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
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
              <v-flex xs12 sm6 md6 lg6>
                <v-menu ref="menu1" v-model="startDateMenu" :close-on-content-click="false" :return-value.sync="date1"
                  transition="scale-transition" offset-y full-width min-width="290px">
                  <template v-slot:activator="{ on }">
                    <v-text-field v-model="date1" label="接收时间" readonly v-on="on"></v-text-field>
                  </template>
                  <v-date-picker v-model="date1" no-title scrollable>
                    <v-spacer></v-spacer>
                    <v-btn text color="primary" @click="startDateMenu = false">取消</v-btn>
                    <v-btn text color="primary" @click="$refs.menu1.save(date1)">确定</v-btn>
                  </v-date-picker>
                </v-menu>
              </v-flex>
              <v-spacer></v-spacer>
              <v-flex xs12 sm6 md6 lg6>
                <v-menu ref="menu2" v-model="endDateMenu" :close-on-content-click="false" :return-value.sync="date2"
                  transition="scale-transition" offset-y full-width min-width="290px">
                  <template v-slot:activator="{ on }">
                    <v-text-field v-model="date2" label="接收时间" readonly v-on="on"></v-text-field>
                  </template>
                  <v-date-picker v-model="date2" no-title scrollable>
                    <v-spacer></v-spacer>
                    <v-btn text color="primary" @click="endDateMenu = false">取消</v-btn>
                    <v-btn text color="primary" @click="$refs.menu2.save(date2)">确定</v-btn>
                  </v-date-picker>
                </v-menu>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="实际费用"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-text-field label="实际实施"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-textarea label="办理过程"></v-textarea>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-textarea label="原因分析"></v-textarea>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-textarea label="结果及建议"></v-textarea>
                <MuseAlert></MuseAlert>
              </v-flex>
            </v-layout>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <!--  -->
        <v-expansion-panel>
          <v-expansion-panel-header>申请人验收</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-layout wrap>
              <v-flex xs12 sm6 md6 lg6>
                <v-radio-group row>
                  <template v-slot:label>
                    <div>是否解决：</div>
                  </template>
                  <v-radio label="已解决" value="0"></v-radio>
                  <v-radio label="未解决" value="1"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
                <v-radio-group row>
                  <template v-slot:label>
                    <div>是否满意：</div>
                  </template>
                  <v-radio label="满意" value="0"></v-radio>
                  <v-radio label="不满意" value="1"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs12 sm6 md6 lg6>
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
            <iframe src="http://www.baidu.com" style="width: 100%"></iframe>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-layout>
  </v-container>
</template>

<script>
  import TypeDialog from "./TypeDialog";
  import HumanDialog from "./HumanDialog";
  import TextfieldReadonly from "./TextfieldReadonly";
  import WanhuaRadio from './WanhuaRadio';
  import MuseAlert from './Alert'
  export default {
    components: {
      TypeDialog,
      HumanDialog,
      TextfieldReadonly,
      WanhuaRadio,
      MuseAlert
    },
    data: () => ({
      panel: [0, 1, 2, 3, 4, 5, 6],
      serviceTypes: ["type1", "type2", "type3", "type4", "type5"],
      typeValue: "",
      dutyValue: "",
      typedialog: false,
      dutydialog: false,
      row: "",
      startDateMenu: false,
      endDateMenu: false,
      date1: new Date().toISOString().substr(0, 10),
      date2: new Date().toISOString().substr(0, 10)
    }),
    methods: {
      typeSelect() {
        // let aaa = 1;
        // this.typeValue = aaa;
        this.typedialog = !this.typedialog;
      },
      dutySelect() {
        this.dutydialog = !this.dutydialog;
      },
      typeDialogSelected(value) {
        console.log("bbbbb", value);
        this.typeValue = value.name;
      },
      dutyDialogSelected(value) {
        console.log("cccc", value);
        this.dutyValue = value;
      }
    }
  };
</script>
<style>
  .container.grid-list-xl .layout .flex {
    padding: 0 12px;
  }

  .v-text-field {
    padding-top: 0;
  }
</style>