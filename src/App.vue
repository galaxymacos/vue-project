<script setup>
  import { ref } from 'vue'
  
  const header = ref('Shopping List App')
  const items = ref([
    {id: 1, label: "10 party hats"},
    {id: 2, label: "2 board games"},
    {id: 3, label: "20 cups"},
    {id: 4, label: "10 plates"},
  ])
  const editing = ref(false)
  const newItem = ref('')
  const newItemHighPriority = ref(false)
  const saveItem = ()=>{
    items.value.push({id: items.value.length + 1, label: newItem.value})
    newItem.value = ""
  }
  const setEditingModel = (e) => {
    editing.value = e
  }
  </script>
  
  <template>
    <div class="header">
      <h1>{{ header }}</h1>
      <button class="btn btn-cancel" v-if="editing" @click="setEditingModel(false)">Cancel</button>
      <button class="btn btn-primary" v-else @click="setEditingModel(true)">Add</button>
    </div>
<!--v-model.lazy can be used to update the value only when the input loses focus.-->
    <form v-on:submit.prevent="saveItem()" class="add-item-form" v-if="editing">
      <input
          v-model.trim="newItem"
          type="text"
          placeholder="Add an item">
      Priority:
      <label><input type="checkbox" v-model="newItemHighPriority">High Priority</label>
      <br>
      <button class="btn btn-primary">Save Item</button>
    </form>
    <ul>
<!-- index in list is the index, in dictionary is the key-->
      <li v-for="({id, label}, index) in items" :key="id">
        {{ label }}
      </li>
    </ul>
    <p v-if="items.length === 0">Nothing to show</p>
  </template>