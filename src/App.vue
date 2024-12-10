<template>
  <div>
    <Nav/>
   <RouterView />

  </div>
</template>

<script>
import { RouterView } from 'vue-router';
import Nav from "../src/views/Nav.vue"
  export default {
components:{
  RouterView,
  Nav
}
  }
</script>

<style lang="scss" scoped>

</style>
