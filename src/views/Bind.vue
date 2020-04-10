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
            <v-select
                :items="items"
                v-model="itemList"
                label="items"
                multiple
            ></v-select>
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card height="500" width="400" color="indigo" class="pa-5" :dark="dark">
                cardcardcarcar
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
      itemList:["first"],
      name:"yjk",
      items:["first","second","third"]
    };
  },
  components: {}
};
</script>

<style scoped lang="stylus"></style>

