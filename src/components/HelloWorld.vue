<template>
  <div class="hello">
    <div id="myChart" :style="{width:'500px', height:'300px'}"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{

    }
  },
  mounted(){
    this.drawLine();
  },
  methods: {
    getVirtulData(year) {
      console.log(1)
    year = year || '2017';
    console.log(this.$echarts)
    var date = +this.$echarts.number.parseDate(year + '-01-01');
    var end = +this.$echarts.number.parseDate((+year + 1) + '-01-01');
    console.log(2)
    var dayTime = 3600 * 24 * 1000;
    var data = [];
    for (var time = date; time < end; time += dayTime) {
        data.push([
            this.$echarts.format.formatTime('yyyy-MM-dd', time),
            Math.floor(Math.random() * 10000)
        ]);
    }
    return data;
},
    drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let chart=document.getElementById('myChart')
        let myChart = this.$echarts.init(chart)
        
        // 绘制图表
        myChart.setOption({
    title: {
        top: 30,
        left: 'center',
        text: '2016年某人每天的步数'
    },
    tooltip: {},
    visualMap: {
        min: 0,
        max: 10000,
        type: 'piecewise',
        orient: 'horizontal',
        left: 'center',
        top: 65,
        textStyle: {
            color: '#000'
        }
    },
    calendar: {
        top: 120,
        left: 30,
        right: 30,
        cellSize: ['auto', 13],
        range: '2016',
        itemStyle: {
            borderWidth: 0.5
        },
        yearLabel: {show: false}
    },
    series: {
        type: 'heatmap',
        coordinateSystem: 'calendar',
        data: this.getVirtulData(2016)
    }
});
    }
  }
}
</script>

<style scoped>

</style>
