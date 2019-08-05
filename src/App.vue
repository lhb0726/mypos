<template>
  <div id="app">
    <left-nav></left-nav>
    <div class="m"></div>
    <router-view/>
  </div>
</template>
<script>
import leftNav from '@/components/common/leftNav'
export default {
  name: 'app',
  components: {
    leftNav,
  }
}
</script>
<style>
.main{
  width: 95%;
  float:left;
  background-color: #EFF2F7;
  height: 100%;
  overflow: hidden;
}
</style>
