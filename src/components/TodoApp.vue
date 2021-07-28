<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>
    
    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter Task" class="form-control">
      <button  @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!-- Task Table -->
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th style="width: 120px" scope="col" class="text-center">Status</th>
          <th style="width: 100px" scope="col" class="text-center">#</th>
          <th style="width: 100px" scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th>{{task.name}}</th>
          <td  class="text-center">
            <span @click="changeStatus(index)" class="pointer">
              {{task.status}}
            </span>
          </td>

          <td style="width: 100px">
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen pointer"></span>
            </div>
          </td>

          <td style="width: 100px">
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {

  data(){
    return {
      task: '',
      editedTask: null,
      availableStatuses: ['To-Do', 'In-Progress', 'Completed'],

      tasks: []
    }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0) return;

      if(this.editedTask === null){
        this.tasks.push({
          name: this.task,
          status: 'To-Do'
        });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = '';
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    changeStatus(index){
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatuses[newIndex];
    }
  }
}
</script>

<style scoped>
  .pointer {
    cursor: pointer;
  }
</style>
