<template>
  <div style="margin-bottom:30px">
    <!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
    <div id="main"  ref="chart" style="width:100%x;height:500px;"></div>
  </div>
</template>

<script>
import echarts from 'echarts'
import 'echarts/map/js/china'

export default {
 
  mounted() {
      this.init()
  },
  methods:{
      init(){
           // 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(this.$refs.chart);

        // 指定图表的配置项和数据
        var option = {
                    title: {
                        // text: '地图',
                        
                    },
                    tooltip: {
                    trigger: 'item',
                    // 地图 : {a}（系列名称），{b}（区域名称），{c}（合并数值）, {d}（无）
                    formatter: '城市:{b}<br/> 数据:{c} (p / km2)'
                    },
                    toolbox: {
                        show: true,
                        orient: 'vertical',
                        left: 'right',
                        top: 'center',
                        feature: {
                            dataView: {readOnly: false},
                            restore: {},
                            saveAsImage: {}
                        }
                    },
                    visualMap: {
                        min: 800,
                        max: 50000,
                        text: ['High', 'Low'],
                        realtime: false,
                        calculable: true,
                        inRange: {
                            color: ['lightskyblue', 'yellow', 'orangered']
                        }
                    },
                    
                    series: [
                        {
                           
                            type: 'map',
                            map:'china',
                            label: {
                            show: true,},
                            data:[
                                {name:'北京',value:30000.6},
                                {name: '深圳', value: 20057.34},
                                {name: '湖北', value: 15477.48},
                                {name: '湖南', value: 31686.1},
                                {name: '上海', value: 6992.6},
                                {name: '浙江', value: 44045.49},
                                {name: '宁夏', value: 44045.49},
                                {name: '新疆', value: 10000.49},
                            ]
                        
                        }
                         ]
                };

        // 使用刚指定的配置项和数据显示图表。
        myChart.setOption(option);
      },
    //   如果有接口  由于异步  this.init()改地方
    //    getList(){
    //         axios.get('http://127.0.0.1:3333/get_lists').then(res=>{
    //             this.lists = res.data;
    //             this.init();
    //         })
    //     }
        
       
  }
}
</script>

<style >


</style>
