<template>
    <div class="mainBody">
      <condition-content></condition-content>
    </div>
</template>

<script>

import conditionContent from './content'
export default {
  name: 'Body',
  components: {
    conditionContent
  }
}
</script>

<style lang="stylus" scoped>

  .mainBody
    width : 100%
    position: absolute
    top: 44px
    bottom: 0
    background: url('../assets/background.png')
    background-repeat : repeat
</style>
