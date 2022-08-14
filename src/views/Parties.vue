<template>
  <div class="EEG">
    <!-- <div id="EEG" style="width:90%;height:600px;"></div> -->
    <div class='GraphSpace'>
      <div id="EEG" style="width:100%;height:1000px;"></div>
    </div>
  </div>
</template>
<style>
body {
  margin:0;
  padding:0;
}
html{
  height:100%;
}
.EEG{
  /* width: 1080px; */
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  /* align-items:center; */
}

.EEG .GraphSpace{
  background-color: #fff;
  border:1px solid #ced4da;
  border-radius:.25rem;
  margin-right: 5px;
  margin-left: 5px;
}

</style>
<script>
import * as echarts from 'echarts';

export default {
  name: 'Parties',
  components: {

  },
  // 用于设定checkbox初始选项
  data () {
    return {
      graph_data:'',
    };
  },
  methods:{
    drawChart() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = echarts.init(document.getElementById("EEG"));
      myChart.hideLoading();
      console.log(this.graph_data[0])
      // this.graph_data[0].children.forEach(function (datum, index) {
      //   index % 2 === 0 && (datum.collapsed = true);
      // });
      // 指定图表的配置项和数据
      let option = {
        tooltip: {
        },
        series: [
          {
            type: 'graph',
            layout: 'force',
            force: {
              // repulsion: 50,
              gravity: 0,
              edgeLength: 50
            },

            nodes: this.graph_data,

            itemStyle: {
              symbolSize: 100
            },
            label: {
              show: true,
              position: "bottom",
              distance: 20,
              fontSize: 10,
              align: "center",
            },

            top: '1%',
            left: '7%',
            bottom: '1%',
            right: '7%',
            roam: true,
          }
        ]
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
      // 点击事件
      myChart.on('click',  (params) => {
        if (params.dataType == 'node') {
          this.$router.push({
            name: 'EntityInstitute',
            params: { name: params.data.name },
          })
        }
      });
    },
  },
  mounted() {
    this.graph_data = require('../assets/twparties_mapped/new_main_table_size.json');
    console.log(this.graph_data)
    this.drawChart();


  }

}
</script>
