<template>
  <div class="page1">
    <div class="container">
      <div class="panel">
        <button @click="switchMode('edit')">编辑</button>
        <button @click="switchMode('read')">阅览</button>
      </div>
      <wj-flex-grid
        :itemsSource="users"
        :initialized="initUsers"
        :allowPinning="allowPinning"
        :isReadOnly="!edit"
        :headersVisibility="headersVisibility"
      >
        <wj-flex-grid-column binding="name" header="name"></wj-flex-grid-column>
        <wj-flex-grid-column binding="age" header="age"></wj-flex-grid-column>
        <wj-flex-grid-column binding="sex" header="sex" :dataMap="sexList"></wj-flex-grid-column>
        <wj-flex-grid-column binding="good" header="good"></wj-flex-grid-column>
      </wj-flex-grid>
      <br />
      <!-- headers visibility -->
      <wj-menu
        :value="headersVisibility"
        :header="'ヘッダー'"
        :itemClicked="itemClicked.bind(this,'headersVisibility')"
      >
        <wj-menu-item :value="0">なし</wj-menu-item>
        <wj-menu-item :value="1">列</wj-menu-item>
        <wj-menu-item :value="2">行</wj-menu-item>
        <wj-menu-item :value="3">すべて</wj-menu-item>
      </wj-menu>
      <v-switch label="allowPinning" v-model="allowPinning"></v-switch>
      <v-radio-group v-model="headersVisibility" row>
        <v-radio label="All" value="3"></v-radio>
        <v-radio label="Row" value="2"></v-radio>
        <v-radio label="Column" value="1"></v-radio>
        <v-radio label="None" value="0"></v-radio>
      </v-radio-group>
      <v-card width="300" flat>
        <v-select
          :items="headersVisibilityList"
          v-model="headersVisibility"
          label="headersVisibility"
          outlined
          dense
          color="pink"
        ></v-select>
      </v-card>
    </div>
  </div>
</template>

<script>
import "@grapecity/wijmo.vue2.grid";
import "@grapecity/wijmo.styles/wijmo.css";
import * as wjcGrid from "@grapecity/wijmo.grid";
export default {
  data() {
    return {
      edit: false,
      users: [],
      data: null,
      sexList: ["man", "woman"],
      headersVisibility: wjcGrid.HeadersVisibility.All,
      allowPinning: true,
      headersVisibilityList: ["All", "Row", "Column", "None"]
    };
  },
  components: {},
  methods: {
    initUsers() {
      this.users = this.createData(30);
    },
    initializeGrid() {
      this.data = this._getData();
    },

    createData(count) {
      let data = [];
      for (let i = 0; i < count; i++) {
        let rowData = {
          name: "yjk",
          age: 10 + i,
          sex: i % 2 == 0 ? "man" : "woman",
          good: i % 2 == 0 ? true : false
        };
        data.push(rowData);
      }
      return data;
    },

    switchMode(mode) {
      if (mode == "edit") {
        this.edit = true;
      } else {
        this.edit = false;
      }
    },
    itemClicked: function(prop, s) {
      if (s.selectedIndex > -1) {
        this[prop] = s.selectedValue;
      }
    }
  }
};
</script>

<style scoped lang="stylus">
.wj-flexgrid
  max-height 500px
.panel
  display flex
  justify-content flex-start
  padding 10px
</style>
