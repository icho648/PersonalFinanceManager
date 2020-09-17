<template>
  <el-main>
    <el-row :gutter="500">
    <el-col :span="6">
      <div class="grid-content bg-purple">
        <div id="myChart" :style="{width: '400px', height: '400px'}"></div>
      </div>
    </el-col>
    <el-col :span="6">
      <div class="grid-content bg-purple">
        <div id="myChart2" :style="{width: '400px', height: '400px'}"></div>
      </div>
    </el-col>
    </el-row>
    <el-row :gutter="500">
    <el-col :span="6">
      <div class="grid-content bg-purple">
        <div id="myChart3" :style="{width: '400px', height: '400px'}"></div>
      </div>
    </el-col>
    <el-col :span="6">
      <div class="grid-content bg-purple">
        <div id="myChart4" :style="{width: '400px', height: '400px'}"></div>
      </div>
    </el-col>
    </el-row>




  </el-main>
</template>

<script>
export default {
  name: 'hello',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      info: null
    }
  },
  mounted() {
    this.drawLine();
    this.axiosTest()
  },
  methods: {
    axiosTest(){
      this.$axios.get('account/list_account').then(response => {
        if (response.data) {
          console.log(response.data)
        }
      }).catch(err => {
        alert('请求失败')
      })
    },
    drawLine() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = this.$echarts.init(document.getElementById('myChart'))
      let myChart2 = this.$echarts.init(document.getElementById('myChart2'))
      let myChart3 = this.$echarts.init(document.getElementById('myChart3'))
      let myChart4 = this.$echarts.init(document.getElementById('myChart4'))
      // 绘制图表
      myChart.setOption({
        title: {text: 'budget'},
        tooltip: {},
        xAxis: {
          data: ["April", "May","June","July"]
        },
        yAxis: {},
        series: [{
          name: 'amount',
          type: 'bar',
          data: [1000, 2000,4000,3000]
        },{
          name:'expense',
          type: 'bar',
          data: [500, 2500,900,5000]
        }]

      });
      myChart2.setOption({
        title: {text: 'daily expense'},
        xAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
        },
        yAxis: {
          type: 'value'
        },
        series: [{
          data: [820, 932, 901, 934, 1290, 1330, 1320],
          type: 'line'
        }]
      });
      myChart3.setOption({
        backgroundColor: '#2c343c',

        title: {
          text: 'account',
          left: 'center',
          top: 20,
          textStyle: {
            color: '#ccc'
          }
        },

        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },

        visualMap: {
          show: false,
          min: 80,
          max: 600,
          inRange: {
            colorLightness: [0, 1]
          }
        },
        series: [
          {
            name: 'balance',
            type: 'pie',
            radius: '55%',
            center: ['50%', '50%'],
            data: [
              {value: 1000, name: 'credit cards'},
              {value: 200, name: 'bund'}

            ].sort(function (a, b) {
              return a.value - b.value;
            }),
            roseType: 'radius',
            label: {
              color: 'rgba(255, 255, 255, 0.3)'
            },
            labelLine: {
              lineStyle: {
                color: 'rgba(255, 255, 255, 0.3)'
              },
              smooth: 0.2,
              length: 10,
              length2: 20
            },
            itemStyle: {
              color: '#c23531',
              shadowBlur: 200,
              shadowColor: 'rgba(0, 0, 0, 0.5)'
            },

            animationType: 'scale',
            animationEasing: 'elasticOut',
            animationDelay: function (idx) {
              return Math.random() * 200;
            }
          }
        ]
      });
      myChart4.setOption({
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b}: {c} ({d}%)'
        },
        legend: {
          orient: 'vertical',
          left: 10,
          data: ['mortage', 'rent', 'shopping', 'clothes']
        },
        series: [
          {
            name: 'amount',
            type: 'pie',
            radius: ['50%', '70%'],
            avoidLabelOverlap: false,
            label: {
              show: false,
              position: 'center'
            },
            emphasis: {
              label: {
                show: true,
                fontSize: '30',
                fontWeight: 'bold'
              }
            },
            labelLine: {
              show: false
            },
            data: [
              {value: 335, name: 'mortage'},
              {value: 310, name: 'rent'},
              {value: 234, name: 'shopping'},
              {value: 135, name: 'clothes'},
            ]
          }
        ]
      })
    }
  }
}
</script>

<style scoped>

</style>
