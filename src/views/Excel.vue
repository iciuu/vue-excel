<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloExcel msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloExcel from '@/components/HelloExcel.vue'

export default {
  name: 'excel',
  components: {
      HelloExcel
  }
}
</script>
