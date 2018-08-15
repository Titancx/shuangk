<template>
  <div style="width:100%;height:305px;" id="china-map"></div>
</template>

<script>
import echarts from 'echarts';
import geoData from './map-data/get-geography-value.js';
export default {
    name:'ChinaMap',
    props: {
        cityData: Array
    },
    data(){
        return{
           
        }
    },
  methods: {
          
  },
  mounted(){
       var convertData = function (data) {
            let res = [];
            let len = data.length;
            console.log(data.length)
            for (var i = 0; i < len; i++) {
                var geoCoord = geoData[data[i].name];
                if (geoCoord) {
                    res.push({
                        name: data[i].name,
                        value: geoCoord.concat(data[i].value)
                    });
                }
            }
            return res;
        };

        var map = echarts.init(document.getElementById('china-map'));
        const chinaJson = require('./map-data/china.json');
        echarts.registerMap('china', chinaJson);
        map.setOption({
            backgroundColor: '#FFF',
            geo: {
                map: 'china',
                label: {
                    emphasis: {
                        show: false
                    }
                },
                itemStyle: {
                    normal: {
                        areaColor: '#EFEFEF',
                        borderColor: '#CCC'
                    },
                    emphasis: {
                        areaColor: '#E5E5E5'
                    }
                }
            },
            visualMap: {  
                    show : true,  
                    x: 'left',  
                    y: 'center',  
                    splitList: [   
                        {start: 500, end:600},{start: 400, end: 500},  
                        {start: 300, end: 400},{start: 200, end: 300},  
                        {start: 100, end: 200},{start: 0, end: 100},  
                    ],  
                    color: ['#5475f5', '#9feaa5', '#85daef','#74e2ca', '#e6ac53', '#9fb5ea']  
                },  
            grid: {
                top: 0,
                left: '2%',
                right: '2%',
                bottom: '0',
                containLabel: true
            },
            series: [{
                type: 'scatter',
                coordinateSystem: 'geo',
                data: convertData(this.cityData),
                symbolSize: function (val) {
                    return val[2] / 10;
                },
                label: {
                    normal: {
                        formatter: '{b}',
                        position: 'right',
                        show: false
                    },
                    emphasis: {
                        show: true
                    }
                },
                itemStyle: {
                    normal: {
                        color: '#0099CC'
                    }
                }
            }]

        });
        window.addEventListener('resize', function () {
            map.resize();
        });
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>

</style>
