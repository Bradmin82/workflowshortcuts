<template>
  <div id="app" class="container mt-5">
    <div class="row">
      <div class="col form-inline">
        <b-form-input v-model="newTask" placeholder="Enter Task" @keyup.enter="add"></b-form-input> 
        <b-button class="ml-2" variant="primary" @click="add">Add</b-button>
      </div>
    </div>
    <div class="row mt-3">
      <div class="col-md-3">
        <div class="p-2 alert alert-secondary">
          <h3>Backlog</h3>
          <draggable class="list-group" :list="arrBacklog" group="tasks">
            <div class="list-group-item" v-for="element in arrBacklog" :key="element.name">
              {{element.name}}
            </div>
          </draggable>
        </div>
      </div>
      <div class="col-md-3">
        <div class="p-2 alert alert-warning">
          <h3>In Progress</h3>
          <draggable class="list-group" :list="arrInProgress" group="tasks">
            <div class="list-group-item" v-for="element in arrInProgress" :key="element.name">
              {{element.name}}
            </div>
          </draggable>
        </div>
      </div>
      <div class="col-md-3">
        <div class="p-2 alert alert-success">
          <h3>Tested</h3>
          <draggable class="list-group" :list="arrTested" group="tasks">
            <div class="list-group-item" v-for="element in arrTested" :key="element.name">
              {{element.name}}
            </div>
          </draggable>
        </div>
      </div>
      <div class="col-md-3">
        <div class="p-2 alert alert-primary">
          <h3>Completed</h3>
          <draggable class="list-group" :list="arrDone" group="tasks">
            <div class="list-group-item" v-for="element in arrDone" :key="element.name">
              {{element.name}}
            </div>
          </draggable>
        </div>
      </div>
    </div>
    <div class="row mb-3">
      <div class="col form-inline">
        <b-form-input v-model="newShortcut1" placeholder="Enter Shortcut" @keyup.enter="add"></b-form-input> 
        <b-button class="ml-2" variant="primary" @click="add">Add</b-button>
      </div>
    </div>
    <div class="row shortcuts-container">
      <draggable class="list-group-s shortcut" :list="shortcuts1" group="shortcuts1">
        <div class="list-group-item-s" v-for="shortcut in shortcuts1" :key="shortcut.id">
          <div class="p-2 alert alert-success">
            <h3>{{shortcut.title}}</h3>
            
                <div style="color: hotpink;">{{shortcut.description}}</div>
            
          </div>
        </div>
      </draggable>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  name: 'App',
  components: {
    draggable
  },
  data() {
    return {
      newTask: "",
      arrBacklog: [
        {name: "Code Sign Up Page"},
        {name: "Test Dashboard"},
        {name: "Style Registration"},
        {name: "Help with Designs"},
      ],
      arrInProgress:[],
      arrTested: [],
      arrDone: [],
      newShortcut1: "",
      shortcuts1: []
    }
  },
  methods: {
    add() {
      if(this.newTask) {
        this.arrBacklog.push({name: this.newTask});
        this.newTask="";
      }
      if(this.newShortcut1) {
        this.shortcuts1.push({title: this.newShortcut1, description: (this.newShortcut1 + ' desc')});
        this.newShortcut1="";
      }
    }
  },
  mounted() {
   fetch('http://localhost:3000/shortcuts')
    .then(res => res.json())
    .then(data => this.shortcuts1 = data)
    .catch(err => console.log(err.message))
  }
}
</script>

<style>
#app {
  margin-top: 60px;
}
#app .shortcuts-container {
  flex-direction: column;
}
</style>
