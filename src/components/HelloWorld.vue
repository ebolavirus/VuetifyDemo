<template>
  <v-container grid-list-xl>
    <v-layout wrap text-center>
      <v-expansion-panels v-model="panel" multiple >
        <v-expansion-panel>
          <v-expansion-panel-header>服务描述</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-flex xs12 sm12 md12>
              <v-text-field label="*服务类型" append-icon="mdi-anchor"></v-text-field>
            </v-flex>
            <v-flex xs12 sm12 md12>
              <v-radio-group v-model="row" row>
                <template v-slot:label>
                  <div>*紧急程度：</div>
                </template>
                <v-radio label="普通" value="1"></v-radio>
                <v-radio label="紧急" value="0"></v-radio>
              </v-radio-group>
            </v-flex>
            <v-flex>
              <v-text-field label="*办公室位置"></v-text-field>
              <v-textarea label="服务内容"></v-textarea>
            </v-flex>
          </v-expansion-panel-content>
          <!-- IT顾问评估 -->
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-header>IT顾问评估</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-flex xs12 sm6>
              <v-text-field label="*服务类型" append-icon="mdi-anchor"></v-text-field>
              <v-radio-group v-model="row" row>
                <template v-slot:label>
                  <div>*紧急程度：</div>
                </template>
                <v-radio label="普通" value="1"></v-radio>
                <v-radio label="紧急" value="0"></v-radio>
              </v-radio-group>
              <v-text-field label="*办公室位置"></v-text-field>
            </v-flex>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    panel: [0,1,2,3,4]
  })
};
</script>
