<template>
  <div>
    <ul>
      <li v-for="todo in doneTodos" :key="todo.text">
        {{ todo.text }}
      </li>
    </ul>
    <button @click="checkAllTodos">Finalizar tudo</button>
  </div>
</template>

<script lang="ts">
/*
### Checklist
[x] Definir o dado `todos`
[x] Preencher os `todos` quando o componente é criado
[x] Exibir em tela apenas `todos` concluídos
[x] Ter um método para concluir os `todos`
[] Mostrar um alerta quando todos os `todos` forem finalizados
```

### Todos
[
  { text: 'Estudar Typescript', done: true },
  { text: 'Lavar os pratos', done: false },
  { text: 'Aprender Nuxt.js', done: true }
]
```
*/

import { defineComponent } from "vue";

interface Todo {
  text: string;
  done: boolean;
}

export default defineComponent({
  data() {
    return {
      todos: [] as Todo[],
    };
  },
  computed: {
    doneTodos(): Todo[] {
      return this.todos.filter((todo) => todo.done);
    },
  },
  watch: {
    todos(newValue: Todo[]) {
      const insFinished = !newValue.some(({ done }) => !done);
      console.log(insFinished);
      if (insFinished) {
        alert("Todos as tasks foram finalizados!");
      }
    },
  },
  created() {
    this.todos = [
      { text: "Estudar Typescript", done: true },
      { text: "Lavar os pratos", done: false },
      { text: "Aprender Nuxt.js", done: true },
    ];
  },
  methods: {
    checkAllTodos() {
      this.todos = this.todos.map(({ text }) => {
        return { text, done: true };
      });
    },
  },
});
</script>
