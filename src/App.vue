<script setup>
  import { ref, computed } from 'vue'
  
  const header = ref('Shopping List App')
  const items = ref([
    {id: 1, label: "10 party hats", purchased: false, highPriority: false},
    {id: 2, label: "2 board games", purchased: false, highPriority: false},
    {id: 3, label: "20 cups", purchased: true, highPriority: false},
    {id: 4, label: "10 plates", purchased: true, highPriority: true},
  ])
  const editing = ref(false)
  const newItem = ref('')
  const newItemHighPriority = ref(false)
  const saveItem = ()=>{
    items.value.push({id: items.value.length + 1, label: newItem.value, purchased: false, highPriority: newItemHighPriority.value})
    newItem.value = ""
    newItemHighPriority.value = false
  }
  const setEditingModel = (e) => {
    editing.value = e
  }
  const togglePurchased = (item) => {
    item.purchased = !item.purchased
  }
  // A more concise way to write computed getters
  const reverseItems = computed(() => [...items.value].reverse())
  const characterCount = computed(() => {
    return newItem.value.length
  })
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
      <button :disabled="newItem.length === 0" class="btn btn-primary">Save Item</button>
    </form>
    <p v-if="editing">{{ characterCount}} / 200</p>
    <ul>
<!-- index in list is the index, in dictionary is the key-->
      <li
          v-for="(item, index) in reverseItems"
          :key="item.id"
          @click="togglePurchased(item)"
          class="static-class"
          :class="{
            strikeout: item.purchased,
            priority: item.highPriority
          }">
        {{ item.label }}
      </li>
    </ul>
    <p v-if="items.length === 0">Nothing to show</p>
  </template>