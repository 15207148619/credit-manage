<template>
  <div >
    <!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
    <div id="main"  ref="chart" style="width: 100%;height:400px;"></div>
  </div>
</template>

<script>
import echarts from 'echarts'

export default {
  name: '',
  data(){
    return{

    }
  },
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
                        text: '一周战绩'
                    },
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                        type: 'cross',
                        label: {
                            backgroundColor: '#6a7985'
                            }
                        }
                    },
                    legend: {
                        data: ['最高借贷金额', '回报率', '业绩领跑', '底薪战队']
                    },
                    toolbox: {
                        feature: {
                            saveAsImage: {}
                        }
                    },
                    grid: {
                        left: '3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },
                    xAxis: [
                        {
                            type: 'category',
                            boundaryGap: false,
                            data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
                        }
                    ],
                    yAxis: [
                        {
                            type: 'value'
                        }
                    ],
                    series: [
                        {
                            name: '最高借贷金额',
                            type: 'line',
                            stack: '总量',
                            areaStyle: {},
                            data: [120, 132, 101, 134, 90, 230, 210]
                        },
                        {
                            name: '回报率',
                            type: 'line',
                            stack: '总量',
                            areaStyle: {},
                            data: [220, 182, 191, 234, 290, 330, 310]
                        },
                        {
                            name: '业绩领跑',
                            type: 'line',
                            stack: '总量',
                            areaStyle: {},
                            data: [150, 232, 201, 154, 190, 330, 410]
                        },
                      
                        {
                            name: '底薪战队',
                            type: 'line',
                            stack: '总量',
                            label: {
                                normal: {
                                    show: true,
                                    position: 'top'
                                }
                            },
                            areaStyle: {},
                            data: [820, 932, 901, 934, 1290, 1330, 1320]
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
