<template>
  <div class="container mx-auto flex items-center w-full h-full">
    <HomeContainer/>
  </div>
</template>

<script>
import HomeContainer from './components/HomeContainer.vue'

export default {
  name: 'App',
  components: {
    HomeContainer
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
}
</style>
