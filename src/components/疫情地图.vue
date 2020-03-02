<template>
  <div class="hello">
    <div ref="mapbox" style="height:1000px;width:1800px">
    </div>
  </div>
</template>

<script>
import echarts from 'echarts';
import 'echarts/map/js/china.js';
import jsonp from 'jsonp';

const option = {
  title: {
    text: '疫情地图',
  },
  series: [{
    name: '确诊人数',
    type: 'map',
    map: 'china',
    label: {
      show: true,
      fontSize: 11,
    },
    zoom: 0.9,
    itemStyle: {
      areaColor: '#eee',
      borderColor: 'gray',
    },
    emphasis: {
      label: {
        color: '#fff',
      },
      itemStyle: {
        areaColor: 'Teal',
        borderColor: 'black',
      },
    },
    data: [],
  }],
  visualMap: [{
    type: 'piecewise',
    show: 'true',
    splitnumber: 6,
    pieces: [
      {min: 10000},
      {min: 1000, max: 9999},
      {min: 100, max: 999},
      {min: 10, max: 99},
      {min: 1, max: 9},
      {max: 0},
    ],
    inRange: {
      symbol: 'rect',
      color: ['Honeydew','Red'],
    },
  }],
  tooltip: {
    toggler: 'item',
  }

}

export default {
  mounted() {
    this.getData();
    this.mychart = echarts.init(this.$refs.mapbox);
    this.mychart.setOption(option);

  },
  methods: {
    getData(){
      jsonp('https://interface.sina.cn/news/wap/fymap2020_data.d.json?_=1580892511427',{},(err,data) => {
        if(!err){
          console.log(data);
          let list = data.data.list.map(item=>({
            name: item.name,
            value: item.value,
          }));
          option.series[0].data = list;
          this.mychart.setOption(option);
        };
      })
    },
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
