<template>
  <h1 class="title">KANPA <span>- 割り勘アプリ -</span></h1> 
</template>
<script>

  export default {
  name: 'Head',
  props: {
    msg: String
  },
  data() {
    return {
      count: 0
    }
  }
}
</script>
<style lang="scss" scoped>
@use "../assets/scss/variable" as v;

.title {
  font-size: 3rem;
  padding-left: 20px;
  color: white;
  background-color: v.$main_bg;
  span {
    font-size: 1.5rem;
  }
}
</style>