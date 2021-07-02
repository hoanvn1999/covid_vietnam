<template>
  <div class="row">
    <div data-aos="fade-right" class="col-md-3 mx-auto">
      <div class="card border-secondary mb-3">
        <div class="card-header text-secondary">Số ca</div>
        <div class="card-body">
          <h5 class="card-title text-center">{{ String(general_info[0]).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</h5>
        </div>
      </div>
    </div>
    <div data-aos="fade-up" class="col-md-3 mx-auto">
      <div class="card border-success mb-3">
        <div class="card-header text-success">Đã khỏi</div>
        <div class="card-body">
          <h5 class="card-title text-center">{{ String(general_info[1]).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</h5>
        </div>
      </div>
    </div>
    <div data-aos="fade-up" class="col-md-3 mx-auto">
      <div class="card border-info mb-3">
        <div class="card-header text-info">Hồi phục</div>
        <div class="card-body">
          <h5 class="card-title text-center">{{ String(general_info[2]).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}</h5>
        </div>
      </div>
    </div>
    <div data-aos="fade-left" class="col-md-3 mx-auto">
      <div class="card border-danger mb-3">
        <div class="card-header text-danger">Tử vong</div>
        <div class="card-body">
          <h5 class="card-title text-center">{{ String(general_info[3]).replace(/(.)(?=(\d{3})+$)/g,'$1,') }}%</h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'General',
  props: {
    general_info: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
