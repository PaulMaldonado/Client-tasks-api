<template>
  <div>
      <div class="container">
          <div class="row mt-4">
              <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4 col-xxl-4">
                  <div class="card">
                      <div class="card-header">Crear tareas</div>
                      <div class="card-body">
                          <form @submit.prevent="createTasks">
                              <div class="form-group mt-3">
                                  <input type="text" 
                                  placeholder="Nombre de la tarea" 
                                  class="form-control"
                                  v-model="tasks.name"
                                  >
                              </div>
                              <div class="form-group mt-3">
                                  <textarea rows="4" 
                                  placeholder="Descripción de la tarea" 
                                  class="form-control"
                                  v-model="tasks.description"
                                  >
                                  </textarea>
                              </div>
                              <div class="form-group mt-3">
                                  <input type="date" 
                                  placeholder="Fecha"
                                  class="form-control"
                                  v-model="tasks.date"
                                  >
                              </div>
                              
                              <template v-if="edit === false">
                                  <button class="btn btn-primary btn-block mt-3">Guardar tarea</button>
                              </template>

                              <template v-else>
                                  <button class="btn btn-secondary">Editar</button>
                              </template>
                          </form>
                      </div>
                  </div>
              </div>

              <div class="col-md-8 col-sm-12 col-lg-8 col-xl-8 col-xxl-8">
                  <div class="card mt-2" v-for="task in tasks" :key="task.id">
                      <div class="card-body">
                          <h5 class="card-title">{{ task.name }}</h5>
                          <p class="card-text">{{ task.description }}</p>
                          <p><strong>{{ task.date }}</strong></p>
                        
                        
                          <button class="btn btn-danger" @click="deleteTask(task.id)">Eliminar</button>
                          <button class="btn btn-secondary" @click="editTask(task.id)">Editar</button>
                      </div>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>

export default {
    data() {
        return {
            tasks: {
                name: '',
                description: '',
                date: ''
            },
            edit: false
        }
    },

    created() {
        this.getAllTask();
    },

    methods: {
      createTasks() {
          const uri = "http://localhost:3000/api/create";

          this.$axios.post(uri, {
              name: this.tasks.name,
              description: this.tasks.description,
              date: this.tasks.date
          })
          .then(result => {
              this.tasks = result.data.results
          })
          .catch(error => {
              console.error(error);
          })

          this.clearInputs();
      },

      getAllTask() {
          this.$axios.get("http://localhost:3000/api/tasks")
            .then(result => {
                this.tasks = result.data.results
                console.log(this.tasks);
            })
            .catch(error => {
                console.error(error);
            });

      },

      deleteTask(id) {
          this.$axios.delete("http://localhost:3000/api/tasks/" + id)
            .then(result => {
                this.tasks = result.splice(id, 1);
            })
      },

      editTask() {
          

      },

      clearInputs() {
        this.tasks.name = "";
        this.tasks.description = "";
        this.tasks.date = "";
      }
    }
}
</script>

<style>

</style>