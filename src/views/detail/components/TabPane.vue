<template>
  <el-table :data="list" border fit highlight-current-row style="width: 100%">
    <el-table-column
      v-loading="loading"
      align="center"
      label="ID"
      width="65"
      element-loading-text="请给我点时间！"
    >
      <template slot-scope="scope">
        <span>{{ scope.row.id }}</span>
      </template>
    </el-table-column>

    <el-table-column width="180px" align="center" label="参数名">
      <template slot-scope="scope">
        <span>{{ scope.row.paramName }}</span>
      </template>
    </el-table-column>

    <el-table-column min-width="300px" align="center" label="参数值">
      <template slot-scope="{row}">
        <span>{{ row.paramValue }}</span>
      </template>
    </el-table-column>

    <el-table-column width="150px" label="评分">
      <template slot-scope="scope">
        <el-rate v-model="scope.row.rate" disabled text-color="#ff9900"></el-rate>
        <!-- <svg-icon v-for="n in +scope.row.rate" :key="n" icon-class="star" /> -->
      </template>
    </el-table-column>
  </el-table>
</template>

<script>

export default {
  props: {
    type: {
      type: String,
      default: 'specification'
    }
  },
  data() {
    return {
      list: null,
      loading: false
    }
  },
  created() {
    this.getList()
  },
  methods: {
    getList() {
      this.loading = true
      this.list = [{
        "id": 1,
        "paramName": "内存",
        "paramValue": "128M",
        "rate": 3
      }, {
        "id": 2,
        "paramName": "存储",
        "paramValue": "1T",
        "rate": 1
      }, {
        "id": 3,
        "paramName": "机身颜色",
        "paramValue": "墨色",
        "rate": 3
      }, {
        "id": 4,
        "paramName": "长度",
        "paramValue": "182cm",
        "rate": 5
      }, {
        "id": 5,
        "paramName": "宽度",
        "paramValue": "10cm",
        "rate": 1
      }, {
        "id": 6,
        "paramName": "厚度",
        "paramValue": "20mm",
        "rate": 4
      }, {
        "id": 7,
        "paramName": "重量",
        "paramValue": "150g",
        "rate": 3
      }, {
        "id": 8,
        "paramName": "分辨率",
        "paramValue": "1080p",
        "rate": 2
      }, {
        "id": 9,
        "paramName": "摄像头",
        "paramValue": "三摄",
        "rate": 4
      }, {
        "id": 10,
        "paramName": "充电接口",
        "paramValue": "type-c",
        "rate": 1
      }];
    }
  }
}
</script>

