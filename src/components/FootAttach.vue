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
              <v-flex xs6>
                <v-text-field label="*服务类型" append-icon="mdi-anchor"></v-text-field>
              </v-flex>
              <v-flex xs6>
                <v-radio-group v-model="row" row>
                  <template v-slot:label>
                    <div>*紧急程度：</div>
                  </template>
                  <v-radio label="普通" value="1"></v-radio>
                  <v-radio label="紧急" value="0"></v-radio>
                </v-radio-group>
              </v-flex>
              <v-flex xs12>
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
                <v-text-field label="预估费用"></v-text-field>
              </v-flex>
              <v-flex xs4>
                <v-text-field label="预估实施"></v-text-field>
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
      serviceTypes: ["type1", "type2", "type3", "type4", "type5"]
    })
  };
</script>