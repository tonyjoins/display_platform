<template>
  <div class="app-container">

    <el-row style="background: #fff; padding: 16px 16px 0; margin-bottom: 32px">
      <el-select v-model="value1" multiple placeholder="请选择地区">
      <el-option
        v-for="item in options_region"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>

    <el-select
      v-model="value2"
      multiple
      collapse-tags
      style="margin-left: 20px"
      placeholder="请选择数据类型"
    >
      <el-option
        v-for="item in options_type"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>

    <!-- <div class="block"> -->
    <!-- <span class="demonstration">  </span> -->
    <el-date-picker
      v-model="value3"
      type="daterange"
      align="right"
      unlink-panels
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
      style="margin-left: 20px"
      :picker-options="pickerOptions"
    >
    </el-date-picker>

    <el-button style="margin-left: 20px">开始清洗</el-button>
    </el-row>  
    

    <div class="Echarts">
        <div id="main" 
            style="width: 600px; height: 400px"
            element-loading-text="拼命加载中"
            element-loading-spinner="el-icon-loading"
            >
        </div>
    </div>

  </div>

  <!-- </div> -->

</template>

<script>
export default {
  data() {
    return {
      options_region: [
        {
          value: "选项1",
          label: "zhejiang_quanshehui",
        },
        {
          value: "选项2",
          label: "jinghua_quanshehui",
        },
      ],
      options_type: [
        {
          value: "选项1",
          label: "负荷",
        },
        {
          value: "选项2",
          label: "天气",
        },
      ],
      pickerOptions: {
        shortcuts: [
          {
            text: "最近一周",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近一个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近三个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              picker.$emit("pick", [start, end]);
            },
          },
        ],
      },

      value1: [],
      value2: [],
      value3: [],
    };
  },
  // watch: {
  //     filterText(val) {
  //         this.$refs.tree2.filter(val);
  //     },
  // },

  methods: {
    // filterNode(value, data) {
    //     if (!value) return true;
    //     return data.label.indexOf(value) !== -1;
    // },

    drawChart() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = this.$echarts.init(document.getElementById("main"));
      // 指定图表的配置项和数据
      let option = {
        title: {
          text: "ECharts 入门示例",
        },
        tooltip: {},
        legend: {
          data: ["销量"],
        },
        xAxis: {
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
        },
        yAxis: {},
        series: [
          {
            name: "销量",
            type: "bar",
            data: [5, 20, 36, 10, 10, 20],
          },
        ],
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    },
  },
  mounted() {
    console.log("1111111111111111");
    this.drawChart();
  },
};
</script>

<style lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;

  .github-corner {
    position: absolute;
    top: 0px;
    border: 0;
    right: 0;
  }

  .chart-wrapper {
    background: #fff;
    padding: 16px 16px 0;
    margin-bottom: 32px;
  }
}

@media (max-width: 1024px) {
  .chart-wrapper {
    padding: 8px;
  }
}
</style>