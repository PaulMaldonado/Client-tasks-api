<template>
  <div>
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
          <a href="#" class="navbar-brand">Task app</a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>

          <div class="collpase navbar-collapse justify-content-end" id="navbarNavDropdown">
              <ul class="navbar-nav"> 
                  <li class="nav-item">
                      <a href="#" class="nav-link active">Inicio</a>
                  </li>

                  <li class="nav-item">
                      <a href="#" class="nav-link active">Lista de tareas</a>
                  </li>

                  <li class="nav-item">
                      <a href="#" class="nav-link active">Crear nueva tarea</a>
                  </li>
              </ul>
          </div>
      </nav>    
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
    .navbar-brand {
        margin-left: 20px;
    }
</style>