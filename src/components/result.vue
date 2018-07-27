<template>
  <div class="result">
    <div class="result-textarea">
      <textarea title="" class="form-control" rows="5" v-model="resultString"></textarea>
    </div>
  </div>
</template>

<script>
import RandExp from 'randexp'
export default {
  name: 'result',
  props: ['original', 'tableName', 'sqlNumber'],
  data () {
    return {
      resultString: ''
    }
  },
  mounted: function () {
    let resultArr = this.original
    let _this = this
    if (this.sqlNumber === '0') {
      this.resultString = '生成sql条数不能为0'
    } else {
      for (let i = 0; i < this.sqlNumber; i++) {
        let rowNameArr = []
        let rowRuleArr = []
        resultArr.forEach(function (item) {
          rowNameArr.push(item.rowName)
          if (item.rowRule !== '') {
            rowRuleArr.push(new RandExp(item.rowRule).gen())
          } else {
            rowRuleArr.push(_this.randomString(true, 2, 10))
          }
        })
        this.resultString += 'INSERT INTO \`' + this.tableName + '\` (' + rowNameArr.join(',') + ') VALUES (' + '\'' + rowRuleArr.join('\',\'') + '\'' + ');\n'
      }
    }
  },
  methods: {
    randomString: function (randomFlag, min, max) {
      let str = ''
      let range = min
      let arr = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
      if (randomFlag) {
        range = Math.round(Math.random() * (max - min)) + min
      }
      for (let i = 0; i < range; i++) {
        let pos = Math.round(Math.random() * (arr.length - 1))
        str += arr[pos]
      }
      return str
    }
  }
}
</script>

<style lang="stylus" scoped>
  .result
    margin : 0 auto 0 auto
    max-width :1600px
    min-width : 600px
    .result-textarea
      width :auto
      margin : 20px 30px 0 30px
      background: #fff
      border-radius: 3px
      box-shadow: 0 2px 3px rgba(0,0,0,.1)
      padding: 20px 20px 20px 20px
</style>
