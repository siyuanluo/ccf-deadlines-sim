<template>
  <section>
    <el-row>
      <a href="/" class="title">Graphics and Robotics Conferences Deadlines</a>
    </el-row>
    <el-row class="subtitle">
      The Conferences are selected by Siyuan Luo and Ce Hao. For Deadline Tracking only.    
    </el-row>
  </section>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      showLatestConf: false,
      showStr: ''
    }
  },
  mounted() {
    this.$http.get('https://api.github.com/repos/ccfddl/ccf-deadlines/commits?page=1&per_page=10').then(response => {
      let len = response.body.length

      for(let i = 0; i < len; i++) {
        let str = response.body[i].commit.message
        let strArr = str.split(' ')
        let idx=str.indexOf('(');
        if(strArr[0].toLowerCase() === 'update' || strArr[0].toLowerCase() === 'add'){
          if(idx !== -1){
            str = str.substr(0, idx)
          }
          this.showStr = str
          this.showLatestConf = true
          break;
        }
      }
    })
  },
}
</script>

<style scoped>
.title{
  font-size: 29px;
  color: #2c3e50;
}
.subtitle{
  padding-top: 15px;
  color: #666666;
}
</style>
