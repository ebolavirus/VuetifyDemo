<template>
  <v-dialog v-model="intypedialog" persistent max-width="900px">
    <v-card>
      <v-card-title>
        <span>变更类型选择列表(类型可行内编辑)</span>
      </v-card-title>
      <v-card-text>
        <small>*特别提醒：正确地选择变更类型将大大加快流程处理速度，如果不清楚该选择何种变更，请致电0535-3388800。</small>
        <v-container grid-list-md>
          <v-layout wrap>
            <v-flex xs12>
              <v-data-table :headers="typeheaders" :items="typedesserts"  @item-selected="itemSelected" @click:row="clickRow" :items-per-page="5"
                class="elevation-1">
                <template v-slot:item.name="props">
                  <v-edit-dialog :return-value.sync="props.item.name" @save="save" @cancel="cancel" @open="open"
                    @close="close"> {{ props.item.name }}
                    <template v-slot:input>
                      <v-text-field v-model="props.item.name" label="Edit" single-line counter>
                      </v-text-field>
                    </template>
                  </v-edit-dialog>
                </template>
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
        <v-btn color="blue darken-1" text @click="intypedialog = false">关闭</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    model: {
      prop: 'typedialog',
      event: 'dialogChanged'
    },
    props: {
      typedialog: {
        type: Boolean,
        default: false
      }
    },
    data: () => ({
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
    computed: {
      intypedialog: {
        get() {
          return this.typedialog
        },
        set(value) {
          this.$emit('dialogChanged', value);
        }
      }
    },
    methods: {
      editItem(aItem) {
        console.log('aaaaa', aItem);
        this.$emit('dialogSelected', aItem);
        this.intypedialog = false;
      },
      clickRow(aItem) {
        console.log("++++++++++++");
        console.log(aItem);
      },
      save() {
        console.log('aItem saved');
      },
      cancel() {
        console.log('aItem canceled');
      },
      open() {
        console.log('aItem opened');
      },
      close() {
        console.log('aItem closed');
      },
      itemSelected(item, value) {
        console.log('itemSelected');
        console.log(item)
      }
    }
  };
</script>