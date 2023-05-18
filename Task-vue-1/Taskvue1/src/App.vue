<template>
  <HelloWorld/>
  <ChangeTab />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ChangeTab from './components/ChangeTab.vue'
export default {
  name: 'App',
  components: {
   HelloWorld, 
   ChangeTab
  }
}
</script>
<style>
</style>
