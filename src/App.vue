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
        <b-form-input v-model="newShortcut" placeholder="Enter Shortcut" @keyup.enter="add"></b-form-input> 
        <b-button class="ml-2" variant="primary" @click="add">Add</b-button>
      </div>
    </div>
    <div class="row">
      <div class="col-md-3">
        <div class="p-2 alert alert-success">
          <h3>Shortcuts</h3>
          <draggable class="list-group shortcut" :list="shortcuts" group="shortcuts">
            <div class="list-group-item" v-for="shortcut in shortcuts" :key="shortcut.id">
              {{shortcut.title}}
              <div style="color: hotpink;">{{shortcut.description}}</div>
            </div>
          </draggable>
        </div>
      </div>
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
      newShortcut: "",
      shortcuts: []
    }
  },
  methods: {
    add() {
      if(this.newTask) {
        this.arrBacklog.push({name: this.newTask});
        this.newTask="";
      }
      if(this.newShortcut) {
        this.shortcuts.push({title: this.newShortcut, description: (this.newShortcut + ' desc')});
        this.newShortcut="";
      }
    }
  },
  mounted() {
   fetch('http://localhost:3000/shortcuts')
    .then(res => res.json())
    .then(data => this.shortcuts = data)
    .catch(err => console.log(err.message))
  }
}
</script>

<style>
#app {
  margin-top: 60px;
}
</style>
