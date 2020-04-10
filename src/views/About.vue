<template>
  <div class="container-fluid">
    <div>
      <wj-input-color :value="clrStart" :value-changed="startColorChanged"></wj-input-color>
      <wj-input-color :value="clrEnd" :value-changed="endColorChanged"></wj-input-color>
    </div>
    <table>
      <tr>
        <td
          v-for="(color,index) in gradient"
          v-bind:style="{backgroundColor:color}"
          v-bind:key="index"
        >&nbsp;</td>
      </tr>
    </table>
    <div id="theColor"></div>
  </div>
</template>

<script>
import "@grapecity/wijmo.styles/wijmo.css";
import "@grapecity/wijmo.vue2.input";
import { Color, animate } from "@grapecity/wijmo";
export default {
  data: function() {
    return {
      clrStart: "red",
      clrEnd: "purple",
      gradient: [],
      interval: null
    };
  },
  methods: {
    startColorChanged: function(s) {
      this.clrStart = s.value;
      this.interpolate();
    },
    endColorChanged: function(s) {
      this.clrEnd = s.value;
      this.interpolate();
    },
    interpolate: function() {
      var c1 = new Color(this.clrStart),
        c2 = new Color(this.clrEnd);

      // calculate new gradient
      this.gradient = [];
      for (let i = 0, cnt = 80; i < cnt; i++) {
        this.gradient.push(Color.interpolate(c1, c2, i / cnt));
      }

      // animate the color
      clearInterval(this.interval);
      let theColor = document.querySelector("#theColor");
      this.interval = animate(pct => {
        theColor.style.background = Color.interpolate(c1, c2, pct).toString();
      }, 2000);
    },
    test:function () {
      
    }
  },
  mounted: function() {
    this.interpolate();
  }
};
</script>

<style lang="css" scoped>
.container-fluid .wj-control {
  margin-bottom: 12px;
}

table {
  width: 100%;
}

#theColor {
  width: 150px;
  height: 150px;
  margin: 12px auto;
  border: 2px solid black;
  background-color: grey;
}
</style>