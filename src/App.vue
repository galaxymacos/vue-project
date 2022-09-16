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
  const newItemPriority = ref("low")
  </script>
  
  <template>
    <h1>{{ header }}</h1>
<!--v-model.lazy can be used to update the value only when the input loses focus.-->
    <input v-model.trim="newItem" type="text" placeholder="Add an item">
    {{ newItem }} Priority:
    <!-- two ways of adding label to the radio button -->
    <label><input type="radio" v-model="newItemPriority" id="low" value="low">Low</label>
    <input type="radio" v-model="newItemPriority" id="high" value="high"><label for="high">high</label>

    <ul>
<!-- index in list is the index, in dictionary is the key-->
      <li v-for="({id, label}, index) in items" :key="id">
        {{ label }}
      </li>
    </ul>
  </template>