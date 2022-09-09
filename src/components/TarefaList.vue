<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="tarefa in lista" :key="tarefa.id">
        <h5>
          {{ tarefa.title }}
          <span class="task-badge right-align">{{ tarefa.project }}</span>
        </h5>
        <button class="btn btn-small" @click="editarClick(tarefa.id)">
          Editar
        </button>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    msg: String,
    lista: Array,
  },
  methods: {
    editarClick(tarefaId) {
      this.$emit('editarClick', tarefaId)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
span {
  background: gray;
  padding: 5px;
  border-radius: 5px;
  margin-left: 15px;
}
</style>
