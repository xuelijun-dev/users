<template>
  <div>
    <h1>用户列表</h1>
    <table>
      <tr>
        <td>编号</td>
        <td>姓名</td>
        <td>年龄</td>
        <td>生日</td>
        <td>操作</td>
      </tr>
      <tr v-for="user in users">
        <td>{{user.id}}</td>
        <td>{{user.name}}</td>
        <td>{{user.age}}</td>
        <td>{{user.birth}}</td>
        <td><a href="javascript:;" @click="delRow(user.id)">删除</a>   <a :href="'#/user/edit?id='+user.id">编辑</a></td>
      </tr>
    </table>
    <a href="#/user/add">添加</a>
    <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: "User",
  data (){
    return {
      users : [{id:1,name:"xiaohei",age:26,birth:"1995-01-17"}]
    }
  },
  methods:{
    findAll(){
      this.$http.get("http://localhost:8090/user/findAll?page=1&rows=10").then((res) =>{
        this.users = res.data.rusults;
      })
    },
    delRow(id){
      console.log(id);
      this.$http.get("http://localhost:8090/user/delete?id="+id).then((res) => {
        if(res.data.success){
          alert(res.data.msg)
          this.findAll();
        }
      })
    }
  },
  created() {
    this.findAll();
  },
  watch:{//监听路由
    $route: {
      handler: function (val,oldVal){
        console.log(val)
        console.log(oldVal)
        if(val.path=='/user'){
          this.findAll();
        }
      },
      //深度观察监听
      deep:true
    }
  }
}
</script>

<style scoped>

</style>
