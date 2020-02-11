<template>
    <div class="container-fluid">
      <div class="row justify-content-center ">
      <div class="card mt-5">
    <h1 class="card-header text-center">TO DO LIST </h1>
    <br/>
    <br />
    <div class="tambah-data">
      <div class="form-tambah card-body">
      <form @submit.prevent="addData">
        <input type="text" placeholder="Judul" v-model="taskData" class="form-control"/>
        <br/>
        <input type="text" placeholder="Mata Kuliah" v-model="coursesData" class="form-control"/>
        <br/>
        <input type="text" placeholder="Batas Waktu" v-model="deadlineData" class="form-control"/>
        <br/>
        <input type="text" placeholder="Deskripsi" v-model="descriptionData" class="form-control"/>
        <br />
        <button class="btn-add" @click="addData">Tambah</button>
      </form>
      </div>
    </div></div>
    <div class="todo-list mt-5 col-4 list-group">
      <div class="list-item" v-for="(item, index) in todoList" :key="index">
        <div class="card-todo ml-5">
          <div class="col-6">
          <h2 style="text-align: left">{{item.task}}</h2>
          <p style="text-align: left">{{item.courses}} | Due Date : {{item.deadline}}</p>
          <p style="text-align: left">{{item.description}}</p>
          </div>
          <div class="col-4">
            <button class="btn-remove" @click="removeData(item)" >DELETE</button>
          </div>
        </div>
      </div>
    </div>
  </div></div>
</template>

<script>
export default {
  data: () => ({
    taskData: '',
    coursesData: '',
    deadlineData: '',
    descriptionData: '',
    todoList: [],
  }),
  created() {
    this.loadlocalStorage();
  },
  watch: {
    todoList() {
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
  },
  methods: {
    addData() {
      if (this.taskData !== '') {
        const date = new Date();
        const dataTask = {
          id: date.getTime(),
          task: this.taskData,
          courses: this.coursesData,
          deadline: this.deadlineData,
          description: this.descriptionData,
          complete: false,
          show: false,
        };
        this.todoList.push(dataTask);
      }
      this.taskData = '';
      this.coursesData = '';
      this.deadlineData = '';
      this.descriptionData = '';
    },
    removeData(item) {
      const index = this.todoList.findIndex((Element) => Element.id === item.id);
      this.todoList.splice(index, 1);
    },
    loadlocalStorage() {
      const ls = JSON.parse(localStorage.getItem('todoList'));
      if (ls == null) {
        return;
      }
      this.todoList = ls;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.card-header{
	background-color: blueviolet;
	color: white;
}
.container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  margin: 10px;
}
.container-fluid{
  min-height: 770px;
}
.tambah-data {
  margin-top: -50px;
  text-align: center;
  background-color: #f5f5f5;
  border-radius:5px;
}
.form-tambah {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  padding-top: 10px;
}
.todo-list {
 border-radius:15px;
}
.card{
  height: 100px;
}
input[type=text] {
  height: 30px;
  margin: 5px;
  padding: 5px;
  cursor: pointer;
  transition: 0.3s;
  width: 450px;
}
input[type=text]:focus {
  border: 2px solid dodgerblue;
  border-radius: 0px;
}
.btn-add{
    background-color: transparent;
    color:#42d100;
    border: 2px solid #42d100;
    border-radius: 0px;
    text-align: center;
    margin: 5px 2px;
    padding: 10px 15px;
    cursor: pointer;
    transition: 0.3s;
    margin: 20px;
    width: 300px;
}
.btn-add:hover{
    background-color: #42d100;
    color: white;
}
.card-todo {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-auto-rows: minmax(10px, auto);
    margin-bottom: 20px;
    background-color: #f5f5f5;
}
.col-8 {
  padding-left: 10px;
  width: 600px;
}
.card-todo:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}
.btn-remove{
    background-color: transparent;
    color:red;
    border: 2px solid red;
    border-radius: 0px;
    text-align: center;
    margin: 5px 2px;
    padding: 10px 15px;
    cursor: pointer;
    transition: 0.3s;
    margin: 20px;
}
.btn-remove:hover{
    background-color: red;
    color: white;
}
</style>