<template>
  <div class="pa-5">
    <h1 class="display-2 pa-5">Bind</h1>
    <v-row>
      <v-col cols="4">
        <v-card height="500" width="400" color="primary" class="pa-5" :dark="dark">
          <h1>card</h1>
          <v-checkbox label="style" v-model="dark"></v-checkbox>
          <v-switch label="switch" v-model="dark" :loading="loading"></v-switch>
          <v-switch label="loading" v-model="loading"></v-switch>
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card height="500" width="400" color="teal" class="pa-5" dark>
          <h2>{{itemList}}</h2>
          <v-select :items="items" v-model="itemList" label="items" multiple></v-select>
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card height="500" width="400" color="indigo" class="pa-5" :dark="dark">
          <p v-for="item in searchList" :key="item.value">{{item.label}}</p>
          <v-card width="100" height="100" v-for="item in searchList" :key="item.value" :color="item.color">
            
          </v-card>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dark: true,
      loading: false,
      itemList: ["first"],
      name: "yjk",
      items: ["first", "second", "third"],
      searchList: [
        {
          value: 0,
          label: "周",
          color:"red"
        },
        {
          value: 2,
          label: "吴",
          color:"white"
        },
        {
          value: 3,
          label: "郑",
          color:"blue"
        },
        {
          value: 4,
          label: "王",
          color:"green"
        }
      ]
    };
  },
  components: {}
};
</script>

<style scoped lang="stylus"></style>

