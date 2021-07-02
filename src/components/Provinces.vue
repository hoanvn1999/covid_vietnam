<template>
  <div data-aos="fade-up">
    <div class="row">
      <div class="col-12">
        <div class="input-group mb-2">
          <div class="input-group-prepend">
            <div class="input-group-text">
              Search
            </div>
          </div>
          <input class="form-control" type="text" v-model="text_search" v-on:input="search()" placeholder="Nhập tỉnh thành bạn muốn tìm kiếm">
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <table class="table table-striped">
          <thead class="bg-primary text-white">
            <tr>
              <th scope="col" class="text-center">Tỉnh thành</th>   
              <th scope="col">Số ca</th>
              <th scope="col">Đã khỏi</th>
              <th scope="col">Hồi phục</th>
              <th scope="col">Tử vong</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="province in provinces_data" :key="province['hc-key']">
              <th scope="row" class="text-center">{{ province.province_name }}</th>
              <td>{{ String(province.value).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
              <td>{{ String(province.socakhoi).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
              <td>{{ String(province.socadangdieutri).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
              <td>{{ String(province.socatuvong).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Provinces',
  data() {
    return {
      text_search: "",
      provinces_data: []
    }
  },
  methods:{
    search() {
      this.provinces_data = [];
      if (this.text_search === '')
        this.provinces_data = this.provinces
      else
        for(let i=0; i<this.provinces.length; i++)
          if(('' + this.provinces[i].province_name).search(this.text_search) !== -1)
            this.provinces_data.push(this.provinces[i]);
    },
  },
  props: {
    provinces: Array
  },
  watch: {
    provinces(val){
      this.provinces_data = val
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
