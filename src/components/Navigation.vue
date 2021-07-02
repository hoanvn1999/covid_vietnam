<template>
  <ul class="nav bg-red justify-content-center position-fixed w-100 p-2">
      <li class="nav-item">
          <a class="nav-link active" href="#general">Thông tin chung</a>
      </li>
      <li class="nav-item">
          <a class="nav-link" href="#provinces">Các tỉnh thành</a>
      </li>
      <li class="nav-item">
          <a class="nav-link" href="#statistic">Thống kê</a>
      </li>
  </ul>
</template>

<script>
export default {
  name: "Resume",
  data() {
    return {};
  },
};
</script>

<style>
  a {
    color: yellow !important;
    font-weight: 500;
  }

  .active {
    color: #fff !important;
    font-weight: 800;
  }

  .bg-red {
    background-color: red;
  }

  .nav {
    z-index: 2;
  }
</style>
