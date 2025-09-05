<template>
  <div>
    <h1>Lista de Tareas</h1>

    <!-- Input para agregar tareas -->
    <input v-model="nuevaTarea" @keyup.enter="agregarTarea" placeholder="Escribe una tarea" />
    <button @click="agregarTarea">Agregar</button>

    <!-- Lista de tareas -->
    <ul>
      <li v-for="(tarea, index) in tareas" :key="index">
        <input type="checkbox" v-model="tarea.completada" />
        <span :class="{ completada: tarea.completada }">{{ tarea.texto }}</span>
        <button @click="eliminarTarea(index)">❌</button>
      </li>
    </ul>

    <!-- Computed: estadísticas -->
    <p>
      Completadas: {{ tareasCompletadas }} /
      Pendientes: {{ tareasPendientes }}
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nuevaTarea: "",
      tareas: JSON.parse(localStorage.getItem("tareas")) || []
    };
  },
  computed: {
    tareasCompletadas() {
      return this.tareas.filter(t => t.completada).length;
    },
    tareasPendientes() {
      return this.tareas.filter(t => !t.completada).length;
    }
  },
  watch: {
    tareas: {
      handler(nuevoValor) {
        localStorage.setItem("tareas", JSON.stringify(nuevoValor));
      },
      deep: true
    }
  },
  methods: {
    agregarTarea() {
      if (this.nuevaTarea.trim()) {
        this.tareas.push({ texto: this.nuevaTarea, completada: false });
        this.nuevaTarea = "";
      }
    },
    eliminarTarea(index) {
      this.tareas.splice(index, 1);
    }
  }
};
</script>

<style>
.completada {
  text-decoration: line-through;
  color: gray;
}
</style>