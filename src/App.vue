<script setup>
  import { ref } from 'vue'
  
  const header = ref('Shopping List App')
  const items = ref([
    {id: 1, label: "10 party hats"},
    {id: 2, label: "2 board games"},
    {id: 3, label: "20 cups"},
    {id: 4, label: "10 plates"},
  ])
  const newItem = ref('')
  const newItemHighPriority = ref(false)
  </script>
  
  <template>
    <h1>{{ header }}</h1>
<!--v-model.lazy can be used to update the value only when the input loses focus.-->
    <form v-on:submit.prevent="items.push({id: items.length + 1, label: newItem})" class="add-item-form">
      <input
          v-model.trim="newItem"
          type="text"
          placeholder="Add an item">
      {{ newItem }} Priority:
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
  </template>