<template>
  <div>
    <main class="col-sm-9 ml-sm-auto col-md-10 pt-3 content" role="main">
          <h2>申请记录</h2>
          <div class="table-responsive">
            <button class="btn btn-success" @click="addApply">增加</button>
            <button class="btn btn-danger" @click="removeApply">删除</button>
            <button class="btn btn-info" @click="updateApply">更新</button>
            <a class="btn btn-success" :href="backendURL + '/apply/download.csv'" download="apply_data.csv" @click="exportApply">导出记录</a>
            <br/>
            <label>已网申：{{appliedCount}}&nbsp;&nbsp;</label><label>总记录：{{totalCount}}</label>
            <table class="table table-striped">
              <thead>
                <tr>
                  <th></th>
                 <th class="ui-state-default sorting">公司及招聘官网 <i class="fa fa-sort clickable-icon" labelname="companyName" aria-hidden="true" @click="setSortKey"></i></th>
                  <th class="ui-state-default sorting">申请日期  <i class="fa fa-sort clickable-icon" labelname="applyDate" aria-hidden="true" @click="setSortKey"></i></th>
                  <th class="ui-state-default sorting">状态  <i class="fa fa-sort clickable-icon" labelname="status" aria-hidden="true" @click="setSortKey"></i></th>
                  <th class="ui-stae-default sorting">备注</th>
                  <th class="ui-stae-default sorting">最后一面的日期</th>
                  <th class="ui-stae-default sorting">预期结果 </th>
                </tr>
              </thead>
              <tbody>
                
                <tr v-for="(item, index) in sortedApply">
                  <th v-if="!flags[index]"><i class="fa fa-square-o" aria-hidden="true"  @click="switchFlag(index)"></i></th>
                  <th v-if="flags[index]"><i class="fa fa-check-square-o" aria-hidden="true"  @click="switchFlag(index)"></i></th>
                  <th v-if="!item.website" class="ui-state-default">{{item.companyName}}</th>
                  <th v-if="item.website" class="ui-state-default"><a :href="'' + item.website" target="_blank">{{item.companyName}}</a></th>
                  <th class="ui-state-default">{{item.applyDate}}</th>
                  <th class="ui-state-default">{{item.status}}</th>
                  <th class="ui-state-default">{{item.remark}}</th>
                  <th class="ui-state-default">{{item.endDate}}</th>
                  <th class="ui-state-default">{{item.anticipate}}</th>
              </tr>
              </tbody>
            </table>
          </div>
    </main>
  </div>
  
        
</template>
<script>
export default {
  props: {
    user: Object,
    flags: Array,
    sortedApply: Array,
    sortBy: String
  },
  data () {
    return {
      backendURL: global.backendURL
    }
  },
  computed: {
    appliedCount: function () {
      if (this.sortedApply.length === 0) {
        return 0
      } else {
        var tmp = 0
        var len = this.sortedApply.length
        for (var i = 0; i < len; i++) {
          var tmpStr = '待网申'
          // console.log(this.sortedApply[i]['status'])
          if (tmpStr !== this.sortedApply[i]['status']) {
            tmp += 1
          }
        }
        return tmp
      }
    },
    totalCount: function () {
      if (this.sortedApply.length === 0) {
        return 0
      } else {
        return this.sortedApply.length
      }
    }
  },
  methods: {
    addApply: function () {
      this.$emit('addApply')
    },
    removeApply: function () {
      this.$emit('removeApply')
    },
    updateApply: function () {
      this.$emit('updateApply')
    },
    exportApply: function (event) {
      this.$emit('exportApply', event)
    },
    switchFlag: function (index) {
      this.$emit('switchFlag', index)
    },
    setSortKey: function (event) {
      // console.log(event.target.getAttribute('labelname'))
      this.$emit('setSortKey', event.target.getAttribute('labelname'))
    }
  }
}
</script>
<style scoped>
@import url('https://cdn.bootcss.com/font-awesome/4.7.0/css/font-awesome.css');
.clickable-icon {
  cursor: pointer;
}

</style>
