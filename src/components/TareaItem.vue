<template>
  <div class="alert alert-warnin mt-3 d-flex justify-content-between align-items-center"
  >
    <p class="m-0" :class="{'tachado': tarea.estado}">{{tarea.texto}}    
    </p>
      <h3>
          <i class="fas fa-undo-alt mx-2 text-success" 
          role="button"
          @click="modificar(tarea.id)"
          v-if="tarea.estado"
          ></i>
          <i class="fas fa-check-circle mx-2 text-success" 
          role="button"
          @click="modificar(tarea.id)"
          v-else
          ></i>
          <i class="fas fa-minus-circle mx-2 text-danger" 
          role="button"
          @click="eliminar(tarea.id)"   
          ></i>
      </h3>
          
  </div>
</template>

<script>
import { inject } from 'vue'


export default {
    props: {
        tarea: {
            type: Object,
            required: true
        },
    },
    setup() {
        const tareas = inject('tareas')

        const eliminar = id => {
            tareas.value = tareas.value.filter(item => item.id !== id)
        }
        const modificar = id => {
            tareas.value = tareas.value.map(item => {
                if(item.id === id){
                    item.estado = !item.estado
                }
                return item
            })
        }
        return {eliminar, modificar}
    }
}
</script>
.<style scoped>
.tachado {
    text-decoration: line-through;
}
</style>
