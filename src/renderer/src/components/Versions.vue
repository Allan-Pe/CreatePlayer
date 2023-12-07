<script setup>
import { reactive } from 'vue'

const versions = reactive({ ...window.electron.process.versions })
</script>

<template>
  <v-container class="fill-height">
    <v-responsive class="text-center fill-height">

      <h1 class="text-h3 font-weight-bold title">Create your player</h1>

      <div style="display: flex;">
        <div class="containerGraph">
          <div cols="auto" style="display: flex; flex-direction: column; align-items: center;">
            <label for="listCate">Liste des compétences</label> <br>
            <input v-model=InputListCate type="text" @keyup.enter="ListOfCate" name="listeCate" placeholder="compétence 1, compétence 2, ..." class="inputCate">
          </div>
          
          <div v-if="isEnter" cols="auto">
            <div id="chart">
              <apexchart type="radar" width="100%" height="350" :options="chartOptions" :series="series"></apexchart>
            </div>
            <div class="statsBlock">
              <h2>Modifier les données du graphique</h2>
              <ul class="points">
                <li v-for="(value, index) in series[0].data" :key="index">
                  <div class="flexStats">
                    <span>{{ TbCate[index] }} : </span>
                    <input class="inputPoints" v-model="series[0].data[index]"/>
                  </div>
                  
                  <input class="slidePoints rangecolor" type="range" v-model="series[0].data[index]" min="0" max="5" step="1" />
                </li>
              </ul>
            </div>
          </div>
        </div>
        <div class="containerGraph">
          <div cols="auto" style="display: flex; flex-direction: column; align-items: center;">
            <label for="listCate">Liste des Techniques</label> <br>
            <input v-model=InputListTech type="text" @keyup.enter="ListOfTech" name="listeCate" placeholder="compétence 1, compétence 2, ..." class="inputCate">
          </div>
          
          <div v-if="isEnter2" cols="auto">
            <div id="chart2">
              <apexchart type="radar" width="100%" height="350" :options="chartOptions2" :series="series2"></apexchart>
            </div>
            <div class="statsBlock">
              <h2>Modifier les données du graphique</h2>
              <ul class="points">
                <li v-for="(value, index) in series2[0].data" :key="index">
                  <div class="flexStats">
                    <span>{{ TbTech[index] }} : </span>
                    <input class="inputPoints" v-model="series2[0].data[index]"/>
                  </div>
                  
                  <input class="slidePoints rangecolor2" type="range" v-model="series2[0].data[index]" min="0" max="5" step="1" />
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </v-responsive>
  </v-container>
</template>

<script>
import VueApexCharts from "vue3-apexcharts";

export default {
  components: {
    apexchart: VueApexCharts,
  },
  computed: {
    
  },
  data() {
    return {
      isEnter: false,
      isEnter2: false,
      InputListCate: "" ,
      InputListTech: "" ,
      chartOptions: {
        chart: {
              height: 350,
              type: 'radar',
            },
            dataLabels: {
              enabled: true
            },
            plotOptions: {
              radar: {
                size: 140,
                polygons: {
                  strokeColors: '#e9e9e9',
                  fill: {
                    colors: ['#f8f8f8', '#fff']
                  }
                }
              }
            },
            title: {
              text: ' '
            },
            colors: ['#0075ff','#EB7628', '#83D45A'],
            markers: {
              size: 4,
              colors: ['#fff'],
              strokeColor: '#0075ff',
              strokeWidth: 2,
            },
            tooltip: {
              y: {
                formatter: function(val) {
                  return val
                }
              }
            },
            xaxis: {
              categories: ["oui","non","oui"]
            },
            yaxis: {
              tickAmount: 7,
              labels: {
                formatter: function(val, i) {
                  if (i % 2 === 0) {
                    return val
                  } else {
                    return ''
                  }
                }
              }
            }
      },
      chartOptions2: {
        chart: {
              height: 350,
              type: 'radar',
            },
            dataLabels: {
              enabled: true
            },
            plotOptions: {
              radar: {
                size: 140,
                polygons: {
                  strokeColors: '#e9e9e9',
                  fill: {
                    colors: ['#f8f8f8', '#fff']
                  }
                }
              }
            },
            title: {
              text: ' '
            },
            colors: ['#9aa1d1','#EB7628', '#83D45A'],
            markers: {
              size: 4,
              colors: ['#fff'],
              strokeColor: '#0075ff',
              strokeWidth: 2,
            },
            tooltip: {
              y: {
                formatter: function(val) {
                  return val
                }
              }
            },
            xaxis: {
              categories: ["oui","non","oui"]
            },
            yaxis: {
              tickAmount: 7,
              labels: {
                formatter: function(val, i) {
                  if (i % 2 === 0) {
                    return val
                  } else {
                    return ''
                  }
                }
              }
            }
      },
      TbCate:[],
      TbTech:[],
      series: [
        {
          name: "series-1",
          data: [],
        },
      ],
      series2: [
        {
          name: "series-1",
          data: [],
        },
      ],
    };
  },
  methods :{
    ListOfCate(){
      this.isEnter = true
      const joursString = this.InputListCate;

      // Check if joursString is defined before using split
      const ListOfCate = joursString ? joursString.split(',') : [];
      this.TbCate = ListOfCate

      this.series[0].data = ListOfCate.map(() => 2);
      return this.chartOptions= {
        chart: {
              height: 350,
              type: 'radar',
            },
            plotOptions: {
              radar: {
                size: 140,
                polygons: {
                  strokeColors: '#e9e9e9',
                  fill: {
                    colors: ['#f8f8f8', '#fff']
                  }
                }
              }
            },
            title: {
              text: ' '
            },
            colors: ['#C61B6A','#EB7628', '#83D45A'],
            markers: {
              size: 4,
              strokeWidth: 2,
            },
            tooltip: {
              y: {
                formatter: function(val) {
                  return val
                }
              }
            },
            xaxis: {
              categories: ListOfCate
            },
            yaxis: {
              tickAmount: 5,
              min: 0,
              max: 5,
              labels: {
                formatter: function(val, i) {
                  if (i % 2 === 0) {
                    return val;
                  } else {
                    return '';
                  }
                }
              }
            }
      }
    },
    ListOfTech(){
      this.isEnter2 = true
      const joursString = this.InputListTech;

      // Check if joursString is defined before using split
      const ListOfTech = joursString ? joursString.split(',') : [];
      this.TbTech = ListOfTech

      this.series2[0].data = ListOfTech.map(() => 2);
      return this.chartOptions2= {
        chart: {
              height: 350,
              type: 'radar',
            },
            plotOptions: {
              radar: {
                size: 140,
                polygons: {
                  strokeColors: '#e9e9e9',
                  fill: {
                    colors: ['#f8f8f8', '#fff']
                  }
                }
              }
            },
            title: {
              text: ' '
            },
            colors: ['#8B008B','#EB7628', '#83D45A'],
            markers: {
              size: 4,
              strokeWidth: 2,
            },
            tooltip: {
              y: {
                formatter: function(val) {
                  return val
                }
              }
            },
            xaxis: {
              categories: ListOfTech
            },
            yaxis: {
              tickAmount: 5,
              min: 0,
              max: 5,
              labels: {
                formatter: function(val, i) {
                  if (i % 2 === 0) {
                    return val;
                  } else {
                    return '';
                  }
                }
              }
            }
      }
    }
  }
}
</script>
<style>
.rangecolor[type="range"] {
  accent-color: #C61B6A;
}
.rangecolor2[type="range"] {
  accent-color: darkmagenta;
}
body{
  background-color: white;
}
#chart{
  text-align: -webkit-center;
  margin: 35px 5%;
}
#chart2{
  text-align: -webkit-center;
  margin: 35px 5%;
}
.containerGraph{
  width: -webkit-fill-available;
}
.flexStats{
  display: flex;
  justify-content: space-between;
}
.inputCate{
  width: 80%;
  border: solid black 1px;
  border-radius: 5px;
  padding: 2px;
}
.inputPoints{
  border: solid gray 1px;
  border-radius: 10px;
  width: 40px;
  text-align-last: center;
}
li{
  width: 250px;
  margin: 20px;
}
.points{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  list-style-type: none;
}
.slidePoints{
  width: -webkit-fill-available;
  color:red !important;
}
.statsBlock{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.title{
  margin-top: 30px;
  margin-bottom: 30px;
  text-align: center;
}
</style>

