<template>
  <div>
    <input v-model="nombre" placeholder="Escribe tu nombre" />

    <!-- Usando propiedad computada -->
    <p>{{ mensajeBienvenida }}</p>

    <!-- Usando método (para comparar) -->
    <p>{{ obtenerBienvenida() }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombre: ''
    }
  },
  computed: {
    mensajeBienvenida() {
      console.log("Computed ejecutado ✅");
      return this.nombre
        ? `Bienvenido, ${this.nombre}!`
        : "Bienvenido, invitado!";
    }
  },
  methods: {
    obtenerBienvenida() {
      console.log("Método ejecutado ⚡");
      return this.nombre
        ? `Bienvenido, ${this.nombre}!`
        : "Bienvenido, invitado!";
    }
  }
}
</script>