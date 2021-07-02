<template>
  <div id="app">
    <navigation />
    <div class="container">
      <div class="text-center"><h1>Thống kê tình hình dịch bệnh Covid-19 tại Việt Nam</h1></div>

      <div id="general" class="col-12">
        <div class="text-center"><h2>Thông tin chung</h2></div>
        <general 
          :general_info = general_info
        />
        <chart 
          :general_info = general_info
        />
      </div>

      <div id="provinces" class="col-12">
        <div class="text-center"><h2>Các tỉnh thành</h2></div>
        <provinces
          :provinces = provinces
        />
      </div>

      <div id="statistic" class="col-12">
        <div class="text-center"><h2>Thống kê trong 7 ngày qua</h2></div>
        <statistical
          :statistic = statistic
        />
      </div>
    </div>
  </div>
</template>

<script>
import Chart from './components/Chart.vue';
import General from './components/General.vue'
import Navigation from './components/Navigation.vue';
import Provinces from './components/Provinces.vue';
import Statistical from './components/Statistical.vue';

export default {
  name: 'App',
  components: {
    General,
    Chart,
    Provinces,
    Statistical,
    Navigation
  },
  data() {
    return {
      general_info: [0,0,0,0],
      provinces: [0],
      statistic: {0: '-'}
    }
  },
  methods: {
    capitlizeString(word, index) {
      return word.charAt(index).toUpperCase() + word.slice(index + 1);
    },
    sort(){
      this.provinces.sort((a, b) => {
        if(Number(a.value) < Number(b.value)) return 1;
        if(Number(a.value) > Number(b.value)) return -1;
        return 0;
      })
    }
  },
  created() {
    this.axios.get('https://api.apify.com/v2/key-value-stores/ZsOpZgeg7dFS1rgfM/records/LATEST').then(response => {
      this.general_info = [response.data.infected, response.data.treated, response.data.recovered, response.data.deceased]
      let data = response.data.detail
      this.provinces = data

      this.axios.get('https://api.apify.com/v2/key-value-stores/p3nS2Q9TUn6kUOriJ/records/LATEST').then(response => {
        let data = response.data.key;
        for(let i=0; i<this.provinces.length; i++) {
          data[i].name = data[i].name.replace('-', ' ')
          this.provinces[i]['province_name'] = this.capitlizeString(data[i].name, 0)  
        }
        this.sort();
      });
    });
    this.axios.get('https://api.quarantine.country/api/v1/spots/week?region=vietnam').then(response => {
      let data = response.data.data;
      this.statistic = data
    });
  }
}
</script>

<style>
  h1 {
    padding: 80px 0 0 0;
    font-weight: 600;
  }

  h2 {
    padding: 80px 0 5px 0;
  }
</style>
