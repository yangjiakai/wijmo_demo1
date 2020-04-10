<template>
  <div class="container-fluid">
    <!-- search box -->
    <div class="row">
      <div class="col-md-6 col-xs-4">
        <input type="text" class="form-control app-pad" placeholder="フィルター" v-model="filter" />
      </div>
      <div class="col-md-6 col-xs-8">
        <wj-collection-view-navigator :cv="collectionView" class="pull-right"></wj-collection-view-navigator>
      </div>
    </div>

    <!-- the grid -->
    <wj-flex-grid
      :itemsSource="collectionView"
      :initialized="initialized"
      class="grid"
      :allowResizing="'Both'"
      :allowMerging="'All'"
      :stickyHeaders="false"
      :allowAddNew="allowAddNew"
      :selectionMode="selectionMode"
      :headersVisibility="headersVisibility"
      :showSelectedHeaders="showSelectedHeaders"
      :showMarquee="showMarquee"
      :allowSorting="false"
      :frozenColumns="3"
      :allowPinning="true"
      :autoRowHeight="true"
      :alternatingRowStep="2"
        
    >
      <wj-flex-grid-column binding="id" header="ID" :width="80"></wj-flex-grid-column>
      <wj-flex-grid-column binding="start" header="開始"></wj-flex-grid-column>
      <wj-flex-grid-column binding="end" header="終了"></wj-flex-grid-column>
      <wj-flex-grid-column binding="country" header="国"></wj-flex-grid-column>
      <wj-flex-grid-column binding="product" header="商品"></wj-flex-grid-column>
      <wj-flex-grid-column binding="color" header="色"></wj-flex-grid-column>
      <wj-flex-grid-column binding="countryId" header="国ID"></wj-flex-grid-column>
      <wj-flex-grid-column binding="productId" header="商品ID"></wj-flex-grid-column>
      <wj-flex-grid-column binding="colorId" header="色ID"></wj-flex-grid-column>
      <wj-flex-grid-column binding="amount" header="金額"></wj-flex-grid-column>
      <wj-flex-grid-column binding="amount2" header="金額2"></wj-flex-grid-column>
      <wj-flex-grid-column binding="discount" header="値引" :width="80"></wj-flex-grid-column>
      <wj-flex-grid-column binding="active" header="有効"></wj-flex-grid-column>
    </wj-flex-grid>

    <!-- commands -->
    <div class="well">
      <div class="grid-sort-group">
        <!-- current selection -->
        <p>
          選択されたセル:
          <b>{{selection | cellRange}}</b>
        </p>

        <!-- data size -->
        <wj-menu
          :value="itemCount"
          :header="'データ数'"
          :itemClicked="itemClicked.bind(this,'itemCount')"
        >
          <wj-menu-item :value="5">5</wj-menu-item>
          <wj-menu-item :value="50">50</wj-menu-item>
          <wj-menu-item :value="500">500</wj-menu-item>
          <wj-menu-item :value="5000">5,000</wj-menu-item>
          <wj-menu-item :value="50000">50,000</wj-menu-item>
          <wj-menu-item :value="100000">100,000</wj-menu-item>
          <wj-menu-item :value="500000">500,000</wj-menu-item>
          <wj-menu-item :value="1000000">1,000,000</wj-menu-item>
        </wj-menu>

        <!-- allow add new -->
        <wj-menu
          :value="allowAddNew"
          :header="'行の追加'"
          :itemClicked="itemClicked.bind(this,'allowAddNew')"
        >
          <wj-menu-item :value="true">許可</wj-menu-item>
          <wj-menu-item :value="false">禁止</wj-menu-item>
        </wj-menu>

        <!-- selection mode -->
        <wj-menu
          :value="selectionMode"
          :header="'選択'"
          :itemClicked="itemClicked.bind(this,'selectionMode')"
        >
          <wj-menu-item :value="0">なし</wj-menu-item>
          <wj-menu-item :value="1">セル</wj-menu-item>
          <wj-menu-item :value="2">セル範囲</wj-menu-item>
          <wj-menu-item :value="3">行</wj-menu-item>
          <wj-menu-item :value="4">行範囲</wj-menu-item>
          <wj-menu-item :value="5">行リスト</wj-menu-item>
        </wj-menu>

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

        <!-- highlight headers -->
        <wj-menu
          :value="showSelectedHeaders"
          :header="'選択されたヘッダー'"
          :itemClicked="itemClicked.bind(this,'showSelectedHeaders')"
        >
          <wj-menu-item :value="0">なし</wj-menu-item>
          <wj-menu-item :value="1">列</wj-menu-item>
          <wj-menu-item :value="2">行</wj-menu-item>
          <wj-menu-item :value="3">すべて</wj-menu-item>
        </wj-menu>

        <!-- show marquee -->
        <wj-menu
          :value="showMarquee"
          :header="'マーキー'"
          :itemClicked="itemClicked.bind(this,'showMarquee')"
        >
          <wj-menu-item :value="true">有効</wj-menu-item>
          <wj-menu-item :value="false">無効</wj-menu-item>
        </wj-menu>

        <!-- data maps -->
        <wj-menu
          :value="dataMaps"
          :header="'データマップ'"
          :itemClicked="itemClicked.bind(this,'dataMaps')"
        >
          <wj-menu-item :value="true">有効</wj-menu-item>
          <wj-menu-item :value="false">無効</wj-menu-item>
        </wj-menu>

        <!-- formatting -->
        <wj-menu
          :value="formatting"
          :header="'書式設定'"
          :itemClicked="itemClicked.bind(this,'formatting')"
        >
          <wj-menu-item :value="true">有効</wj-menu-item>
          <wj-menu-item :value="false">無効</wj-menu-item>
        </wj-menu>

        <br />
        <br />

        <!-- testing the object model -->
        <button class="btn btn-danger" @click="toggleColumnVisibility()">先頭列の表示を切り替え</button>
        <button class="btn btn-default" @click="changeColumnSize()">先頭列の幅を変更</button>
        <button class="btn btn-default" @click="toggleRowVisibility()">先頭行の表示を切り替え</button>
        <button class="btn btn-default" @click="changeRowSize()">先頭行の高さを変更</button>
        <button class="btn btn-default" @click="changeDefaultRowSize()">行の既定の高さを変更</button>
        <button class="btn btn-default" @click="changeScrollPosition()">スクロール位置を変更</button>
      </div>
    </div>
  </div>
</template>

<script>
import "@grapecity/wijmo.styles/wijmo.css";
import * as wjcCore from "@grapecity/wijmo";
import * as wjcGrid from "@grapecity/wijmo.grid";
import { getCountries, getProducts, getColors, getData } from "./data";
import "@grapecity/wijmo.vue2.grid";
import "@grapecity/wijmo.vue2.input";
export default {
  created: function() {
    this.dataArray = getData(this.itemCount);
  },
  data() {
    return {
      dataMaps: true,
      formatting: true,
      filter: "",
      selection: null,
      allowAddNew: false,
      selectionMode: wjcGrid.SelectionMode.CellRange,
      headersVisibility: wjcGrid.HeadersVisibility.All,
      showSelectedHeaders: wjcGrid.HeadersVisibility.None,
      showMarquee: false,
      itemCount: 500,
      collectionView: new wjcCore.CollectionView(),
      dataArray: null
    };
  },
  watch: {
    dataMaps: function() {
      console.log("dataMaps watcher");
      this._updateDataMaps();
    },
    dataArray: function(newVal, oldVal) {
      console.log("dataArray watcher");
      this.collectionView.sourceCollection = newVal;
      let flex = this.flex;
      // if it's the first assignment to dataArray
      if (oldVal == null && flex) {
        // make columns 25% wider (for readability and to show how)
        for (let i = 0; i < flex.columns.length; i++) {
          flex.columns[i].width = flex.columns[i].renderSize * 1.25;
        }
      }
      this.updateDataMapSettings();
    },
    itemCount: function(newVal) {
      console.log("itemCount watcher");
      this.dataArray = getData(newVal);
    },
    formatting: function() {
      this._updateFormatting();
    },
    filter: function() {
      this._applyFilter();
    }
  },
  methods: {
    initialized: function(flex) {
      this.flex = flex;
      this.selection = this.flex.selection;
      this.flex.selectionChanged.addHandler((s, e) => {
        this.selection = e.range;
      });
      this.flex.select(new wjcGrid.CellRange(0, 0));
    },
    updateDataMapSettings: function() {
      this._updateDataMaps();
      this._updateFormatting();
    },
    toggleColumnVisibility: function() {
      let flex = this.flex,
        col = flex.columns[0];
      col.visible = !col.visible;
    },
    changeColumnSize: function() {
      let flex = this.flex,
        col = flex.columns[0];
      col.visible = true;
      col.width = col.width < 0 ? 60 : -1;
      col = flex.rowHeaders.columns[0];
      col.width = col.width < 0 ? 40 : -1;
    },
    toggleRowVisibility: function() {
      let flex = this.flex,
        row = flex.rows[0];
      row.visible = !row.visible;
    },
    changeRowSize: function() {
      let flex = this.flex,
        row = flex.rows[0];
      row.visible = true;
      row.height = row.height == null ? 80 : null;
      row = flex.columnHeaders.rows[0];
      row.height = row.height == null ? 80 : null;
    },
    changeDefaultRowSize: function() {
      let flex = this.flex;
      flex.rows.defaultSize = flex.rows.defaultSize == 28 ? 65 : 28;
    },
    changeScrollPosition: function() {
      let flex = this.flex;
      if (flex.scrollPosition.y == 0) {
        let sz = flex.scrollSize;
        flex.scrollPosition = new wjcCore.Point(-sz.width / 2, -sz.height / 2);
      } else {
        flex.scrollPosition = new wjcCore.Point(0, 0);
      }
    },
    // apply/remove data maps
    _updateDataMaps: function() {
      let flex = this.flex;
      if (flex) {
        let colCountry = flex.columns.getColumn("countryId"),
          colProduct = flex.columns.getColumn("productId"),
          colColor = flex.columns.getColumn("colorId");
        if (colCountry && colProduct && colColor) {
          if (this.dataMaps) {
            colCountry.showDropDown = true; // show drop-down for countries
            colProduct.showDropDown = false; // don't show it for products
            colColor.showDropDown = false; // or colors (just to show how)
            colCountry.dataMap = this._buildDataMap(getCountries());
            colProduct.dataMap = this._buildDataMap(getProducts());
            colColor.dataMap = this._buildDataMap(getColors());
          } else {
            colCountry.dataMap = null;
            colProduct.dataMap = null;
            colColor.dataMap = null;
          }
        }
      }
    },

    // build a data map from a string array using the indices as keys
    _buildDataMap: function(items) {
      let map = [];
      for (let i = 0; i < items.length; i++) {
        map.push({ key: i, value: items[i] });
      }
      return new wjcGrid.DataMap(map, "key", "value");
    },

    // apply/remove column formatting
    _updateFormatting: function() {
      let flex = this.flex;
      if (flex) {
        let fmt = this.formatting;
        this._setColumnFormat("amount", fmt ? "c" : null);
        this._setColumnFormat("amount2", fmt ? "c" : null);
        this._setColumnFormat("discount", fmt ? "p0" : null);
        this._setColumnFormat("start", fmt ? "t" : null);
        this._setColumnFormat("end", fmt ? "t" : null);
      }
    },
    _setColumnFormat: function(name, format) {
      let col = this.flex.columns.getColumn(name);
      if (col) {
        col.format = format;
      }
    },
    // apply filter (applied on a 500 ms timeOut)
    _applyFilter: function() {
      if (this.filterTimeOut) {
        clearTimeout(this.filterTimeOut);
      }
      this.filterTimeOut = setTimeout(() => {
        this.filterTimeOut = null;
        if (this.collectionView) {
          let cv = this.collectionView;
          if (cv) {
            if (cv.filter != this.filterFunction) {
              cv.filter = this.filterFunction;
            } else {
              cv.refresh();
            }
          }
        }
      }, 500);
    },
    itemClicked: function(prop, s) {
      if (s.selectedIndex > -1) {
        this[prop] = s.selectedValue;
      }
    },
    filterFunction: function(item) {
      let f = this.filter;
      if (f && item) {
        // split string into terms to enable multi-field searches such as 'us gadget red'
        let terms = f.toUpperCase().split(" ");

        // look for any term in any string field
        for (let i = 0; i < terms.length; i++) {
          let termFound = false;
          for (let key in item) {
            let value = item[key];
            if (
              wjcCore.isString(value) &&
              value.toUpperCase().indexOf(terms[i]) > -1
            ) {
              termFound = true;
              break;
            }
          }

          // fail if any of the terms is not found
          if (!termFound) {
            return false;
          }
        }
      }

      // include item in view
      return true;
    }
  },
  filters: {
    // formats grid selection range to display its value to a user
    cellRange: function(value) {
      let rng = "";
      if (value instanceof wjcGrid.CellRange) {
        rng = "(" + value.row + ";" + value.col + ")";
        if (!value.isSingleCell) {
          rng += "-(" + value.row2 + ";" + value.col2 + ")";
        }
      }
      return rng;
    }
  }
};
</script>

<style scoped lang="css">
.wj-flexgrid {
  height: 400px;
  margin: 6px 0;
}

.grid-sort-group .wj-menu,
.grid-sort-group .btn {
  margin: 2px 2px 2px 0;
}
</style>
