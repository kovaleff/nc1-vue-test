<template>
  <div id="app">
    <el-container v-loading="loading">
      <el-header>Header</el-header>
      <main-dashboard v-bind:houses="houses" @filtered="filterHandler"></main-dashboard>
    </el-container>
  </div>
</template>

<script>
import MainDashboard from './components/MainDashboard.vue';

export default {
  name: 'app',
  components: {
    MainDashboard
  },
  data(){
    return {
      houses:[],
      loading: true
    };
  },
  methods:{
    getData(url){
      fetch(url)
          .then(res => res.json())
          .then(({data}) => {
            this.houses = data
          });
        this.$data.loading = false;
    },
    constructLink(url, filterData){
      if(Object.keys(filterData).length === 0){
        return url;
      } else {
        url = url + '?filter='
        for(let key in filterData){
          if(['name','bedrooms', 'bathrooms','storeys', 'garages','price'].includes(key) && filterData[key]){
            let minPrice = 0;
            let maxPrice = 0;
            switch (key){
              case name:
                url += `${key}:${encodeURI(filterData[key])},`;
                break;
              case 'price':
                [minPrice,maxPrice] = filterData[key].split('-');
                url += `${key}:${minPrice}-${maxPrice},`;
                break;
              default:
                url += `${key}:${filterData[key]},`;
            }
          }
        }
        url= url.slice(0, -1);
      }
      return url;
    },
    filterHandler(filterData){
      const link = this.constructLink(process.env.VUE_APP_ROOT_API, filterData);
      this.getData(link);
    }
  },
  mounted() {
    this.getData(process.env.VUE_APP_ROOT_API);
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.el-header{
  background-color: #42b983;
}
.el-aside{
  background-color: antiquewhite;
}
.el-main{
  background-color: aqua;
}
</style>
