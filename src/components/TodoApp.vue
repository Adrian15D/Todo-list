<template>
  <div class="container">
    <h2 class="text-center mt-5">MI LISTA DE TAREAS</h2>

    <!--Input-->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Ingresa una tarea" class="form-control">
      <button @click="submitTask" class="btn btn-success rounded-0">INGRESAR</button>
    </div>

    <!--Tabla para las tareas-->
    <table class="table table-hover mt-5">
  <thead>
    <tr>
      <th scope="col">TAREA</th>
      <th scope="col">ESTADO</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td>
        <span :class="{'finished': task.status === 'Terminado'}">{{ task.name }}</span>
      </td>
      <td style="width: 120px">
        <span @click="changeStatus(index)" class="pointer" :class="{'text-danger' : task.status === 'Por hacer','text-warning': task.status == 'En progreso','text-success': task.status == 'Terminado'}">{{ firstCharUpper(task.status) }}</span>
      </td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa-solid fa-pen-to-square"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="fa-solid fa-eraser"></span>
        </div>
      </td>
    </tr>
  </tbody>
</table>
</div>
</template>

<script>


export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task: '',
      editedTask: null,
      avalibleStatues:['Por hacer','En progreso','Terminado'],
      tasks: [

      ]
    }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0 ) return;

      if(this.editedTask === null){
      this.tasks.push({
        name : this.task,
        status : 'Por hacer'
      });
    }else{
      this.tasks[this.editedTask].name = this.task;
      this.editedTask = null;
    }


      this.task = '';
    },
  
  deleteTask(index){
    this.tasks.splice(index, 1);
    },

  
  changeStatus(index){
    let newIndex = this.avalibleStatues.indexOf(this.tasks[index].status)
   if(++newIndex > 2)newIndex = 0;
   this.tasks[index].status = this.avalibleStatues[newIndex];
    },

  editTask(index){
    this.task = this.tasks[index].name;
    this.editedTask = index;
    },
    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);

    }
  }
};
</script>


<style scoped>
.pointer {
  cursor: pointer;
}

.finished {
  text-decoration: line-through;
}
</style>
