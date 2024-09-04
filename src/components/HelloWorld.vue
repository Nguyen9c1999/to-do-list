<template>
  <div class="p-2">
    <h1 style="text-align: center" >TO DO LIST</h1>
    <input type="text" class="mb-2" v-model="content">
    <br>
    <button type="button" class="btn btn-primary" @click="add()">Thêm</button>
    <table class="table mt-2">
      <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">content</th>
        <th>Trạng thái</th>
        <th scope="col">Handle</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(work,index) in lists" :key="index">
        <th scope="row">{{index+1}}</th>
        <td :class="{'strikethrough':work.status}">{{work.content}}</td>
        <td>
          <input type="checkbox" v-model="work.status">
        </td>
        <td>
          <button type="button" class="btn btn-success" :disabled="work.status" @click="openModal(work,index)">Edit</button>
          <button type="button" class="btn btn-danger ml-2" @click="deleteWork()">Xóa</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
  <el-dialog
     v-model="isOpen"
      title="Tips"
      width="500"

  >
    <input type="text" class="mb-2" v-model="contentEdit">
    <br>
    <button type="button" class="btn btn-primary" @click="edit()">EDIT</button>
  </el-dialog>

</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      lists:[],
      isOpen:false,
      content:'',
      contentEdit:'',
      indexEdit: null
    }
  },
  methods:{
    add(){
      if(!this.content){
       alert('vui lòng nhập to do list')
        return
      }
      this.lists = [{content: this.content , status: false},...this.lists]
      this.content = ''
    },
    edit(){
      if(!this.contentEdit){
        alert('vui lòng nhập to do list')
        return
      }
      this.lists[this.indexEdit].content = this.contentEdit
      this.isOpen = false;
    },
    deleteWork(index){
      this.lists.splice(index,1)
    },
    openModal(work, index){
      this.isOpen = true;
      this.contentEdit = work.content;
      this.indexEdit = index
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.strikethrough {
  text-decoration: line-through;
}
</style>
