<template>
    <section id="main">
    <h1>My To-Do List</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>
    <ul>
      <li v-for="item in tickedTasks" :key="item.id">
        <to-do-item :label="item.label" :done="item.done" :id="item.id"></to-do-item>
      </li>
    </ul>
    <ul>
      <li v-for="(item, key) in untickedTasks" :key="key">
        <to-do-item :label="item.label" :done="item.done" :id="item.id"></to-do-item>
      </li>
    </ul>
    </section>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue'
import ToDoForm from './components/ToDoForm';
import uniqueId from 'lodash.uniqueid'

export default {
  name: 'App',
  components: {
    ToDoItem,
    ToDoForm
  },
 data() {
    return {
      ToDoItems: [
        { id:uniqueId('todo-'), label: 'Learn Vue', done: false },
        { id:uniqueId('todo-'), label: 'Create a Vue project with the CLI', done: true },
        { id:uniqueId('todo-'), label: 'Have fun', done: true },
        { id:uniqueId('todo-'), label: 'Create a to-do list', done: false },
        { id:uniqueId('todo-'), label: 'Add a 5th to-do item', done: false }
      ]
    };
  },
  methods: {
    addToDo(toDoLabel) {
      //console.log('To-do added:' + toDoLabel);
      this.ToDoItems.push({id:uniqueId('todo-'), label: toDoLabel, done: false});
    }
  },
  computed: {
    untickedTasks() {
      return this.ToDoItems.filter((task) => {
        return !task.done
      })
    },
    tickedTasks() {
        return this.ToDoItems.filter((task) => {
          return task.done
        })
    }
  }
};
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;    
}

body { background-color: #F3F3FF; }

#app {
    display: flex;
    justify-content: center;
    padding: 20px;
    color: #30363D;
}

#main {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    max-width: 375px;
    padding: 30px;
    text-align: left;
    border-radius: 5px;
    background-color: white;
    box-shadow: 0 1px 1px rgba(46, 54, 61,0.11), 
        0 2px 2px rgba(46, 54, 61,0.11), 
        0 4px 4px rgba(46, 54, 61,0.11), 
        0 6px 8px rgba(46, 54, 61,0.11),
        0 8px 16px rgba(46, 54, 61,0.11);
}

h1 {
    margin-bottom: 8px;
    font-weight: 900;   
}

form {
    display: flex;
    flex-direction: column;
}

form:after {
    content:'';
    height: 1px;
    width: 100%;
    margin-top: 20px;
    margin-bottom: 20px;
    background-color: #30363D;
}

form input {
    border: solid 1px #30363D;
    padding: 7px;
    outline: none;
    margin-top: 5px;
    margin-bottom: 10px;
    box-shadow: 0 0 0 2px rgba(31, 111, 235, 0);
    transition: 120ms;
    font-family: inherit;
}

form input:focus {
    border-color: #1F6FEB;
    box-shadow: 0 0 0 2px rgba(31, 111, 235, 0.2);  
}

form button {
    margin-top: 10px;
    background-color: #1F6FEB;
    color: white;
    text-transform: uppercase;
    font-weight: 600;
    padding: 12px 0;
    border: none;
    border-radius: 4px;
    box-shadow: 0 1px 1px rgba(0,0,0,0.11), 
      0 2px 2px rgba(0,0,0,0.11), 
      0 4px 4px rgba(0,0,0,0.11), 
      0 6px 8px rgba(0,0,0,0.11),
      0 8px 16px rgba(0,0,0,0.11);
    cursor: pointer;
    transition: all 120ms;
    outline: none;
}

form button:hover { background-color: darken(#1F6FEB, 10%); }

form button:focus {
    box-shadow: 0 1px 1px rgba(0,0,0,0.11),
        0 0 0 2px rgba(31, 111, 235, 0.2),
        0 2px 2px rgba(0,0,0,0.11), 
        0 4px 4px rgba(0,0,0,0.11), 
        0 6px 8px rgba(0,0,0,0.11),
        0 8px 16px rgba(0,0,0,0.11);
}

ul { list-style-type: none; }
ul:before { font-weight: 900; }
ul:first-of-type:before { content: 'Done'; }
ul:last-of-type:before { content: 'To Do'; }
ul + ul { margin-top: 10px; }

ul label {
    position: relative;
    display: inline-flex;
    align-items: center;
    padding-left: calc(15px + 10px);
    cursor: pointer;
    width: 100%;
}

ul label span {
    font-size: 12px;
    font-weight: bold;
    margin-left: 5px;
    display: inline-block;
}

ul label:after {
    content: '';
    height: 1px;
    width: calc(100% - 30px);
    background-color: #2c3e50;
    position: absolute;
    opacity: 0;
}

ul label:before {
    position: absolute;
    background-color: #FAFAFA;
    display: flex;
    align-items: center;
    align-content: center;
    justify-content: center;
    left: 0;
    content: url("data:image/svg+xml,%0A%3Csvg width='12px' height='9px' viewBox='0 0 12 9' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Cg id='Page-1' stroke='none' stroke-width='1' fill='none' fill-rule='evenodd'%3E%3Cpath d='M4.78794643,8.90625 C4.96651786,8.90625 5.11830357,8.84375 5.24330357,8.71875 L5.24330357,8.71875 L6.15401786,7.80803571 L11.0022321,2.95982143 C11.1272321,2.83482143 11.1897321,2.68303571 11.1897321,2.50446429 C11.1897321,2.32589286 11.1272321,2.17410714 11.0022321,2.04910714 L11.0022321,2.04910714 L10.0915179,1.13839286 C9.96651786,1.01339286 9.81473214,0.950892857 9.63616071,0.950892857 C9.45758929,0.950892857 9.30580357,1.01339286 9.18080357,1.13839286 L9.18080357,1.13839286 L4.78794643,5.53794643 L2.81919643,3.5625 C2.69419643,3.4375 2.54241071,3.375 2.36383929,3.375 C2.18526786,3.375 2.03348214,3.4375 1.90848214,3.5625 L1.90848214,3.5625 L0.997767857,4.47321429 C0.872767857,4.59821429 0.810267857,4.75 0.810267857,4.92857143 C0.810267857,5.10714286 0.872767857,5.25892857 0.997767857,5.38392857 L0.997767857,5.38392857 L3.421875,7.80803571 L4.33258929,8.71875 C4.45758929,8.84375 4.609375,8.90625 4.78794643,8.90625 Z' id='' fill='%23FFFFFF' fill-rule='nonzero'%3E%3C/path%3E%3C/g%3E%3C/svg%3E");
    height: 15px;
    width: 15px;
    border-radius: 2px;
    box-shadow: 0 0 0 1px #30363D;
    transition: all 120ms;
}

input[type="checkbox"] {
    position: absolute;
    left: -9999px;
    cursor: pointer;
}

input:checked + label { color: lighten(#30363D, 60%); }
input:checked + label:after { opacity: 1; }
input:checked + label:before {             
    position: absolute;
    left: 0;
    height: 15px;
    width: 15px;
    box-shadow: 0 0 0 1px darken(#1F6FEB, 10%);
    background-color: #1F6FEB;
}
</style>
