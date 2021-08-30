<template>
  <div class="container ">
    <h1 class="text-center mt-5">My Vue Todo App</h1>

    <!-- Input -->
    <div class="row mt-5">
      <div class="col-md-8 mx-auto">
        <div class="d-flex">
          <input v-model="task" type="text" name="" id="" class="form-control" placeholder="Enter task">
          <button @click="submitTask" class="btn btn-success rounded-0">Submit</button>
        </div>
      </div>
    </div>

    <!-- Task Table -->
    <div class="row">
      <div class="col-md-8 mx-auto">
      <table class="table table-bordered mt-5">
        <thead>
          <tr>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col" class="text-center">#</th>
            <th scope="col" class="text-center">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>{{task.name}}</td>
            <td>
              <span class="pointer" @click="changeStatus(index)">
                {{task.status}}
              </span>
            </td>
            <td>
              <div class="text-center">
                <a href="#" @click="updatetask(index)"><span class="fa fa-pen"></span></a>
              </div>
            </td>
            <td>
              <div class="text-center">
                <a href="#" @click="deletetask(index)"><span class="fa fa-trash"></span></a>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      </div>
    </div>


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
      editTask : null,
      availableStatus : ['To-do','In-progress','Finished'],
      tasks:[
        {
          name: 'Steal bananas from the store',
          status: 'To-do'
        },
        {
          name: 'Eat 1kg chocolate in 1 houre',
          status: 'In-progress'
        }
      ]
    }
  },
  methods: {
    // Add a new Task
    submitTask(){
      if (this.task.length === 0) return;

      if(this.editTask === null){
        this.tasks.push({
          name: this.task,
          status: "to-do"
        });
      }else{
        this.tasks[this.editTask].name = this.task;
        this.editTask = null;
      }

      this.task = "";
    },

    //Delete Task
    deletetask(index){
     this.tasks.splice(index, 1)
    },

    //Update Task
    updatetask(index){
      this.task = this.tasks[index].name;
      this.editTask = index;
    },

    //Change Status
    changeStatus(index){
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0; 
      this.tasks[index].status = this.availableStatus[newIndex];
    }
  }

  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer{
  cursor: pointer;
}
</style>
