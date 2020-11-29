<template>
<div class="container">
  <form>
    <div class="row d-flex justify-content-center align-items-center">
      <div class="col-lg-4 text-center shadow my-5">
          <div class="bg-wrapper">
            <h1 class="text-dark">Tasks</h1>
            <div class="input-group mb-3">
            <input
                type="text"
                class="form-control"
                placeholder="Add a new task"
                aria-label="Recipient's username"
                aria-describedby="button-addon2"
                v-model="tasks"
            />
            <div class="input-group-append">
                <button
                class="btn btn-outline-primary"
                type="button"
                id="button-addon2"
                @click="addTodo()"
                >
                Add
                </button>
            </div>
            </div>
          </div>
      </div>
    </div>
  </form>

  <div class="row d-flex justify-content-center align-items-center">
      <div class="col-lg-4 d-flex justify-content-center">
          <button @click="filterTodos" :class="btnClass">All</button>
          <button @click="filterTodos" :class="btnClass">Completed</button>
          <button @click="filterTodos" :class="btnClass">Uncompleted</button>
      </div>
  </div>

  <div class="row d-flex flex-column justify-content-center align-items-center">
      <div v-for="task in todosFiltered" :key="task.id" class="col-lg-4">
        <Todo :id="task.id" :text="task.task" :completedTask="task.completed" :myFunc="checkTodo" :myOther="deleteTodo" />
      </div>
    <div>
        <label><input class="mx-3" type="checkbox" :checked="!anyremaining" @change="checkAllTodos">Check all</label>
    </div>
  </div>
  <small class="d-block position-absolute bg-success p-1 rounded text-light" style="bottom: 20px;">{{rest}} Items left</small>
</div>
</template>

<script>
import Todo from '@/components/share-tools/Todo'

export default {
  name: "Form",
  components: {
      Todo
  },
  props: {
      defClass: {
          type: String,
          default: ''
      },
      btnClass: {
          type: String,
          default: 'btn btn-light text-secondary'
      }
  },
  data() {
      return {
          tasks: '',
          todos: [],
          icon: 'check',
          filter: 'all'
      }
  },
  methods: {
    addTodo() {
        this.todos.push({
            task: this.tasks,
            completed: false,
            id: Math.random()*1000
        });
        this.tasks = ''
    },
    checkTodo(id){
        
        this.todos.filter((todo)=>{
            return todo.id === id ? todo.completed = !todo.completed : false
        })
        
    },
    deleteTodo(id) {
        const newTodos = this.todos.filter((todo) => {
            return todo.id !== id
        })
        this.todos = newTodos;
    },
    filterTodos(e) {
        this.filter = e.target.innerText
    },
    checkAllTodos() {
        this.todos.forEach((todo) => {
            todo.completed = event.target.checked
        });
    }
  },
  computed: {
      rest() {
          return this.todos.filter(todo => !todo.completed).length
      },
      anyremaining() {
          return this.rest != 0
      },
      todosFiltered() {
          if(this.filter === 'All'){
              return this.todos
          } else if(this.filter === 'Completed') {
              return this.todos.filter(todo => todo.completed)
          } else if(this.filter === 'Uncompleted') {
              return this.todos.filter(todo => !todo.completed)
          }
          return this.todos
      }
  },
};
</script>