<template>
    <div class="header">
      <div>
        <img class="header-img" src="../assets/logo.png"/>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style lang="stylus" scoped>
  .header
    overflow: hidden
    background-color: #fff
    height: 44px;
    font-size: 15px;
    font-weight: 500
    border-bottom: 1px solid rgba(0,0,0,.22)
    padding: 0 20px 0 20px;
    .header-img
      height: 44px
      margin-left: 10%

</style>
