<script>
import ProductItem from "@/components/ProductItem.vue";

export default {
  components: {ProductItem},
  data() {
    return {
      title: '',
      body: '',
      items: [],
      removeItems: [],
    }
  },

  methods: {
    setItems() {
      try {
        if (localStorage.items) {
          this.items = JSON.parse(localStorage.items)
        }
        if (localStorage.removeItems) {
          this.removeItems = JSON.parse(localStorage.removeItems)
        }
      } catch (e) {
      }
    },
    removeItem(item) {
      this.items = this.items.filter(el => el.id !== item.id)
      this.removeItems = [...this.removeItems, item]
      this.saveItemsOnLocalStorage()
      this.saveRemoveItemsOnLocalStorage()
    },
    onSubmit() {
      this.items = [...this.items, {id: Date.now(), title: this.title, body: this.body}]
      this.title = ''
      this.body = ''
      this.saveItemsOnLocalStorage()
    },
    saveItemsOnLocalStorage() {
      localStorage.setItem('items', JSON.stringify(this.items))
    },
    saveRemoveItemsOnLocalStorage() {
      localStorage.setItem('removeItems', JSON.stringify(this.removeItems))
    },
  },
  mounted() {
    this.setItems()
  },
}
</script>

<template>
  <div class="app">
    <header>
      <div class="container">
        header
      </div>
    </header>
    <main>
      <div class="container">
        <form v-on:submit.prevent="onSubmit">
          <h1 class="title">Введите чтобы добавить продукт</h1>
          <div v-show="title==='' || body===''" style="color: red">
            Пожалуйста введите название товара или его описание
          </div>
          <div>
            <div>Название</div>
            <input type="text" v-model="title"/>
          </div>
          <div>
            <div>Описание</div>
            <input type="text" v-model="body"/>
          </div>
          <input :disabled="title==='' || body===''" type="submit">
        </form>
        <h2 class="title">Список продуктов</h2>
        <div class="list">
          <div v-show="items.length === 0 && removeItems.length === 0">Список продуктов пока пуст</div>
          <ProductItem v-for="item in items" :item="item" @remove="removeItem"/>
          <ProductItem v-for="item in removeItems" :item="item" :deletedItem="true"/>
        </div>
      </div>
    </main>
    <footer>
      <div class="container">
        footer
      </div>
    </footer>
  </div>
</template>

<style>
.app {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1 1 0;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 50px 0;
}

input {
  width: 100%;
  margin-bottom: 15px;
  padding: 10px;
  border: 2px solid blue;
}

.list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

footer, header {
  background: blue;
  color: white;
  text-align: center;
  font-size: 50px;
  text-transform: uppercase;
}

.title {
  margin-bottom: 15px;
}

input[type=submit] {
  background: blue;
  color: white;
  transition: all 0.3s ease;
}

input[type=submit]:hover {
  background: #111177;
  border-color: #111177;
}

input[type=submit]:disabled {
  opacity: 0.5;
  background: #111177;
  border-color: #111177;
}


</style>
