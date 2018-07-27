<template>
    <div class="condition">
      <div class="condition-content">
        <div class="main">
          <div class="form-inline">
            <div class="form-group">
              <label>表名：</label>
                <input class="form-control" v-model="tableName" placeholder=""/>
            </div>
            <button class="btn btn-primary" @click="handleNextClick">下一步</button>
          </div>
        </div>
        <div class="condition-row" v-if="show">
          <table class="table table-hover">
            <thead>
              <tr>
                <th>字段名</th>
                <th>正则</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item of conditionData " v-bind:key="item.id">
                <td>
                    <input v-model="item.rowName" class="form-control" placeholder=""/>
                </td>
                <td>
                    <input v-model="item.rowRule" class="form-control" placeholder=""/>
                </td>
              </tr>
            </tbody>
          </table>
          <div class="condition-row-btn">
            <input title=""   v-model="sqlNumber" type="number" class="form-control condition-row-btn-input"/>
            <span class="condition-row-btn-span">条</span>
            <button class="btn btn-primary" @click="handleIncreaseClick">增加一行</button>
            <button class="btn btn-success" @click="handleCreateClick">生成数据</button>
          </div>
        </div>
      </div>
        <result :original="conditionData" :tableName="tableName" :sqlNumber="parseInt(sqlNumber)"  v-if="showResult"></result>
    </div>
</template>

<script>
import Result from './result'
export default {
  name: 'conditionContent',
  data () {
    return {
      show: false,
      tableName: '',
      conditionData: [],
      resultData: [],
      showResult: false,
      sqlNumber: '1'
    }
  },
  methods: {
    handleNextClick: function () {
      if (this.tableName === '') {
        this.tableName = 'defaultTableName'
      }
      this.show = true
      if (this.conditionData.length === 0) {
        this.conditionData.push({
          id: 0,
          rowName: '',
          rowRule: ''
        })
      } else {
        this.conditionData = [{
          id: 0,
          rowName: '',
          rowRule: ''
        }]
      }
    },
    handleIncreaseClick: function () {
      this.conditionData.push({
        id: this.conditionData.length,
        rowName: '',
        rowRule: ''
      })
    },
    handleCreateClick: function () {
      this.showResult = false
      this.conditionData.forEach(function (item, index) {
        if (item.rowName === '') {
          item.rowName = 'defaultRowName' + index
        }
      })
      this.$nextTick(() => {
        this.showResult = true
      })
    }
  },
  components: {
    Result
  }
}
</script>

<style lang="stylus" scoped>
  .condition
    width :100%
    background: url('../assets/background.png')
    background-repeat : repeat
    .condition-content
      margin : 0 auto 0 auto
      max-width :1600px
      min-width : 600px
      .main
        width :auto
        margin : 20px 30px 0 30px
        background: #fff
        border-radius: 3px
        box-shadow: 0 2px 3px rgba(0,0,0,.1)
        padding: 20px 20px 20px 20px
        .form-group
          margin-right :10px
      .condition-row
        width :auto
        margin : 20px 30px 0 30px
        background: #fff
        border-radius: 3px
        box-shadow: 0 2px 3px rgba(0,0,0,.1)
        padding: 20px 20px 20px 20px
        label
          width : 100%
        .condition-row-btn
          text-align: right
          .condition-row-btn-input
            width: 100px
            display: inline
            vertical-align: middle
          .condition-row-btn-span
            margin-right: 20px
            vertical-align: middle
</style>
