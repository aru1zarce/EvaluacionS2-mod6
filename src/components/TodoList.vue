<template>
    <div>
      <h1>Lista de Tareas</h1>
      <input v-model="newTask" placeholder="Agregar nueva tarea" />
      <button @click="addTask">Agregar Tarea</button>
  
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <input 
            v-model="task.text" 
            @blur="updateTask(index)" 
            :disabled="!task.editing" 
          />
          <button @click="editTask(index)">
            {{ task.editing ? 'Guardar' : 'Editar' }}
          </button>
          <button @click="deleteTask(index)">Eliminar</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newTask: '',
        tasks: []
      };
    },
    methods: {
      addTask() {
        if (this.newTask.trim() !== '') {
          this.tasks.push({ text: this.newTask, editing: false });
          this.newTask = '';
        }
      },
      editTask(index) {
        this.tasks[index].editing = !this.tasks[index].editing;
        if (!this.tasks[index].editing) {
          this.updateTask(index); // Guardar cambios al salir del modo de edición
        }
      },
      updateTask(index) {
        // Aquí podrías agregar lógica adicional si necesitas validar el texto
        this.tasks[index].editing = false;
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      }
    }
  };
  </script>
  
  <style scoped>
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    margin: 10px 0;
  }
  </style>