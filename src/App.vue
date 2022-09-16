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
  </script>
  
  <template>
    <h1>{{ header }}</h1>
<!--v-model.lazy can be used to update the value only when the input loses focus.-->
    <input v-model.lazy="newItem" type="text" placeholder="Add an item">
    {{ newItem }}
    <ul>
<!-- index in list is the index, in dictionary is the key-->
      <li v-for="({id, label}, index) in items" :key="id">
        {{ label }}
      </li>
    </ul>
  </template>