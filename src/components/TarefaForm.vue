<template>
  <!-- FORM -->
  <div>
    <h2>{{ titulo }}</h2>
    <input
      type="text"
      name="title"
      id="title"
      placeholder="Entre com a tarefa"
      :value="title"
      @input="form.title = $event.target.value"
    />
    <input
      type="text"
      name="project"
      placeholder="Entre com um projeto"
      :value="project"
      @input="form.project = $event.target.value"
    />

    <button @click="salvaTarefa">{{ btn }}</button>
  </div>
</template>

<script>
export default {
  props: ['titulo', 'title', 'project', 'btn', 'id'],
  data: () => {
    return {
      ListaDeTarefas: ['A', 'B', 'C'],
      form: {
        title: 'teste',
        project: 'Estudo',
      },
    }
  },
  methods: {
    salvaTarefa() {
      const novaTarefa = {
        title: this.form.title,
        project: this.form.project,
        date: new Date().toLocaleDateString('pt'),
      }
      if (this.btn == 'Adicionar') {
        novaTarefa.date = new Date().toLocaleDateString('pt')
        this.$emit('salvarClick', novaTarefa)
      } else {
        novaTarefa.id = this.id
        this.$emit('alterarClick', novaTarefa)
      }
    },
  },
}
</script>
