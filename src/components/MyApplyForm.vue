<template>
  <div>
    <!--<div class="form-close"><i class="fa fa-times-circle" aria-hidden="true"></i></div>-->
    <form class="apply-form">
      <div class="form-group">
        <label for="company-name">公司<i class="fa fa-asterisk" aria-hidden="true"></i></label>
        <input type="text" v-model="companyName" class="form-control" id="company-name" placeholder="比如，阿里">
      </div>
      <div class="form-group">
        <label for="website">公司招聘网站（可选）</label>
        <input type="text" v-model="website" class="form-control" id="website" placeholder="可以直接从浏览器上粘贴过来">
      </div>
      <div class="form-group">
        <label for="apply_date">申请日期<i class="fa fa-asterisk" aria-hidden="true"></i></label>
        <input type="date" v-model="applyDate" class="form-control" id="apply_date" placeholder="比如，2017-09-04">
      </div>
      <div class="form-group">
        <label for="end_date">结束日期（可选）</label>
        <input type="date" v-model="endDate" class="form-control" id="end_date" placeholder="比如，2017-09-04">
      </div>
      <div class="form-group">
        <label for="status">当前状态<i class="fa fa-asterisk" aria-hidden="true"></i></label>
        <select id="status" class="form-control" v-model="status">
          <option value="待网申">待网申</option>
          <option value="已网申">已网申</option>
          <option value="已笔试">已笔试</option>
          <option value="面试中">面试中</option>
          <option value="拿到offer">拿到offer</option>
          <option value="壮烈牺牲">壮烈牺牲</option>
        </select>
        <!-- <input type="text" v-model="status"  class="form-control" id="status" placeholder="比如，HR面结束"> -->
      </div>
      <div class="form-group">
        <label for="remark">备注（可选）</label>
        <input type="text" v-model="remark" class="form-control" id="remark" placeholder="比如，面试日期，笔试日期">
      </div>
      <div class="form-group">
        <label for="anticipate">面试表现（可选）</label>
        <input type="text" v-model="anticipate" class="form-control" id="anticipate" placeholder="给自己的面试表现打个分吧(10分为满分），比如，9分">
      </div>
      <div class="form-group">
        <label for="result">结果（可选）</label>
        <input type="text" v-model="result" class="form-control" id="result" placeholder="比如，拿到offer">
      </div>
      <button type="submit" class="btn btn-default" @click="submitApply">提交</button>
      <button class="btn btn-default" @click="closeForm">取消</button>
    </form>
  </div>
  
</template>
<script>
export default {
  props: {
    user: Object,
    flags: Array,
    selected: Number
  },
  data () {
    var companyName, website, applyDate, endDate, status, remark, anticipate, result, applyId
    if (this.selected !== null) {
      companyName = this.user.apply[this.selected].companyName
      website = this.user.apply[this.selected].website
      applyDate = this.user.apply[this.selected].applyDate
      endDate = this.user.apply[this.selected].endDate
      status = this.user.apply[this.selected].status
      remark = this.user.apply[this.selected].remark
      anticipate = this.user.apply[this.selected].anticipate
      result = this.user.apply[this.selected].result
      applyId = this.user.apply[this.selected].applyId
    }
    return {
      companyName: companyName,
      website: website,
      applyDate: applyDate,
      endDate: endDate,
      status: status,
      remark: remark,
      anticipate: anticipate,
      result: result,
      applyId: applyId
    }
  },
  methods: {
    closeForm: function () {
      this.$emit('closeForm')
    },
    submitApply: function () {
      var submitData = {
        // userId: this.userId,
        userId: this.user.userId,
        applyId: this.applyId,
        companyName: this.companyName,
        website: this.website,
        applyDate: this.applyDate,
        endDate: this.endDate,
        status: this.status,
        remark: this.remark,
        anticipate: this.anticipate,
        result: this.result
      }
      // console.log(submitData)
      this.$emit('submitApply', submitData)
    }
  }
}
</script>
<style scoped>
  .apply-form {
    width: 50%;
    /*float: right;*/
    margin: 0 auto;
    padding: 5%;
    border: 1px solid black;
    border-radius: 3%;
  }
</style>
