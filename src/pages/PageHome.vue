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
      <TarefaList
        msg="Welcome to Your Vue.js App"
        :lista="ListaDeTarefas"
        @editarClick="recebiEditar"
      />
    </div>

    <!-- FORM -->
    <div v-show="exibir.form">
      <TarefaForm
        :titulo="'ABC'"
        :title="form.title"
        :project="form.project"
        :btn="form.btn"
        :id="form.id"
        @salvarClick="recebiSalvar"
        @alterarClick="recebiAlterar"
      />
    </div>
  </div>
</template>

<script>
import TarefaForm from '@/components/TarefaForm.vue'
import TarefaList from '../components/TarefaList.vue'
import TasksApi from '../TasksApi.js'

export default {
  components: {
    TarefaList,
    TarefaForm,
  },
  data: () => {
    return {
      ListaDeTarefas: ['A', 'B', 'C'],
      exibir: {
        lista: true,
        fora: false,
      },
      form: {
        id: '',
        titulo: '',
        title: 'teste',
        project: 'Estudo',
        btn: 'Adicionar',
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
      this.form.btn = 'Adicionar'
    },
    recebiSalvar(novaTarefa) {
      TasksApi.addTasks(novaTarefa, () => {
        this.exibir.form = false
        this.exibir.lista = true
        this.listaTarefas()
      })
    },
    recebiEditar(tarefaId) {
      TasksApi.getTask(tarefaId, (task) => {
        this.form.title = task.title
        this.form.project = task.project
        this.form.id = tarefaId
        this.form.btn = 'Editar'
        this.exibir.form = true
        this.exibir.lista = false
      })
    },
    recebiAlterar(tarefa) {
      TasksApi.updateTasks(tarefa, () => {
        this.listaTarefas()
        this.exibir.form = false
        this.exibir.lista = true
      })
    },
  },
}
</script>

<style></style>
