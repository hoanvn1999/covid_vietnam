<template>
  <div data-aos="fade-in">
    <vc-donut :sections="sections">Việt Nam</vc-donut>
    <div class="pt-4 text-center">Biểu đồ thống kê số ca covid tại Việt Nam</div>
  </div>
</template>

<script>
export default {
  name: 'Chart',
  data() {
    return {
      sections: [{ value: 100 }]
    }
  },
  props: {
    general_info: Array
  },
  methods: {
    ratio(a, b) {
      return a/b*100;
    }
  },
  watch: {
    general_info(val) {
      this.sections = [
        { color: '#dc3545', value: this.ratio(val[3], val[0]) },
        { color: '#198754', value: this.ratio(val[1], val[0]) }, 
        { color: '#0dcaf0', value: this.ratio(val[2], val[0]) }
      ] 
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
