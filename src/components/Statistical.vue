<template>
  <div data-aos="flip-up" class="row">
    <div class="col-12">
      <table class="table table-striped">
        <thead class="bg-primary text-white">
          <tr>
            <th scope="col" class="text-center">Ngày</th>   
            <th scope="col">Tổng số ca</th>
            <th scope="col">Đã khỏi</th>
            <th scope="col">Hồi phục</th>
            <th scope="col">Tử vong</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="date in dates" :key="date.date">
            <th scope="row" class="text-center">{{ date.date }}</th>
            <td>{{ String(date.total_cases).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
            <td>{{ String(date.total_cases - date.recovered - date.deaths).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
            <td>{{ String(date.recovered).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
            <td>{{ String(date.deaths).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Statistical',
  data() {
    return {
      dates: []
    }
  },
  props: {
    statistic: Object
  },
  watch: {
    statistic(val){
      Object.keys(val).forEach(date => {
        let value = val[date];
        value['date'] = date;
        this.dates.push(value)
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
