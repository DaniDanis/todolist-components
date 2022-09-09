<template>
  <div id="app">
    <nav class="orange darken-2">
      <div class="nav-wrapper"></div>
    </nav>
    <img alt="Vue logo" src="../assets/logo.png" />

    <div v-show="exibir.lista" style="padding: 20px">
      <button @click="mostrarCadastro">Adicionar</button>
    </div>

    <!-- lista -->
    <div v-show="exibir.lista">
      <TarefaList msg="Welcome to Your Vue.js App" :lista="ListaDeTarefas" />
    </div>

    <!-- FORM -->
    <div v-show="exibir.form">
      <h2>Cadastrar Tarefa</h2>
      <input
        type="text"
        name="title"
        id="title"
        placeholder="Entre com a tarefa"
        v-model="form.title"
      />
      <input
        type="text"
        name="project"
        v-model="form.project"
        placeholder="Entre com um projeto"
      />

      <button @click="salvaTarefa">Salvar</button>
    </div>
  </div>
</template>

<script>
import TarefaList from '../components/TarefaList.vue'
import TasksApi from '../TasksApi.js'

export default {
  components: {
    TarefaList,
  },
  data: () => {
    return {
      ListaDeTarefas: ['A', 'B', 'C'],
      exibir: {
        lista: true,
        fora: false,
      },
      form: {
        title: 'teste',
        project: 'Estudo',
      },
    }
  },
  created() {
    this.listaTarefas()
  },
  methods: {
    listaTarefas() {
      TasksApi.getTasks((data) => {
        this.ListaDeTarefas = data
      })
    },
    mostrarCadastro() {
      this.exibir.form = true
      this.exibir.lista = false
    },
    salvaTarefa() {
      this.exibir.form = false
      this.exibir.lista = true
      const novaTarefa = {
        title: this.form.title,
        project: this.form.project,
        date: new Date().toLocaleDateString('pt'),
      }
      TasksApi.addTasks(novaTarefa, () => {
        this.listaTarefas()
      })
    },
  },
}
</script>

<style></style>
