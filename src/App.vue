<template>
  <div id="app">
    <Header></Header>
    <Body></Body>
  </div>
</template>

<script>
import Header from './components/Header'
import Body from './components/Body'
export default {
  name: 'App',
  components: {
    Header,
    Body
  }
}
</script>

<style lang="stylus" scoped>

</style>
