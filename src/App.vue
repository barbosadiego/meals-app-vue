<template>
  <div id="app">
    <main>
      <TopBar @initSurprise="initSurprise" @activeSearch="handleSearch"/>
      <Modal
        :idMeal="idMeal"
        v-if="isModalActive"
        @close="isModalActive = false"
        @addItem="addItem"
      />
      <transition>
        <SystemMessage v-if="msg.active" :msg="msg"/>
      </transition>
      <Favorites
        :favorites="favorites"
        @removeItem="removeItem"
        @mealItem="handleMeal"
      />
      <Meals v-if="!isSearching" @addItem="addItem" @mealItem="handleMeal" />
      <MealsSearch v-else :searchItem="searchItem" @addItem="addItem" @mealItem="handleMeal"/>
    </main>
  </div>
</template>

<script>
import TopBar from '@/components/TopBar.vue';
import Favorites from '@/components/Favorites.vue';
import Meals from '@/components/Meals.vue';
import Modal from '@/components/Modal.vue';
import SystemMessage from '@/components/SystemMessage.vue';
import MealsSearch from '@/components/MealsSearch.vue';

export default {
  name: 'App',
  components: {
    TopBar,
    Favorites,
    Meals,
    Modal,
    SystemMessage,
    MealsSearch,
  },
  data() {
    return {
      favorites: [],
      isModalActive: false,
      idMeal: null,
      msg: {message: '', alert: false, active: false},
      savedIds: [],
      isSearching: false,
      searchItem: '',
    };
  },
  methods: {
    handleSearch(item){
      this.isSearching = true;
      this.searchItem = item;
    },
    async initSurprise(){
      try {
        const data = await fetch('https://www.themealdb.com/api/json/v1/1/random.php');
        const response = await data.json();

        this.isModalActive = true;
        this.idMeal = response.meals[0].idMeal
        
      } catch (error) {
        console.log(error)
      }
    },
    handleMeal(id) {
      this.idMeal = id;
      this.isModalActive = true;
    },
    addItem(item) {
      if(!this.savedIds.includes(item.idMeal)){
        this.savedIds.push(item.idMeal)
        this.favorites.unshift(item);
        localStorage.setItem('favorites-meals', JSON.stringify(this.favorites));
        this.sendMessage('Item added!')
      } else {
        this.sendMessage('This recipe has already been include!', true)
      }
    },
    removeItem(item) {
      this.favorites = this.favorites.filter(
        (meal) => meal.idMeal !== item.idMeal,
      );
      localStorage.setItem('favorites-meals', JSON.stringify(this.favorites));
    },
    getItemStorage() {
      const meals = JSON.parse(localStorage.getItem('favorites-meals')) ?? [];
      return meals;
    },
    sendMessage(text, alert){
      this.msg.active = true;
      this.msg.message = text;
      this.msg.alert = alert || false;
      this.clearMessage()
    },
    clearMessage(){
      setTimeout(() => {
        this.msg.active = false;
        this.msg.alert = false;
        this.msg.message = '';
      }, 1500)
    },
    loadMealsId(){
      const data = this.getItemStorage()
      data.forEach((item) => this.savedIds.push(item.idMeal))
    }
  },
  mounted() {
    this.favorites = this.getItemStorage();
    this.loadMealsId()
  },
};
</script>

<style lang="scss">
:root {
  --primary-100: #e6f0ff;
  --primary-200: #b4d3fe;
  --primary-300: #82b6fd;
  --primary-400: #5098fc;
  --primary-500: #03449d;
  --primary-600: #034caf;
  --primary-700: #02367d;
  --primary-800: #01214b;
  --primary-900: #000b19;
  --grey-50: #f8fafc;
  --grey-100: #f1f5f9;
  --grey-200: #e2e8f0;
  --grey-300: #cbd5e1;
  --grey-400: #94a3b8;
  --grey-500: #64748b;
  --grey-600: #475569;
  --grey-700: #334155;
  --grey-800: #1e293b;
  --grey-900: #0f172a;
  --black: #222;
  --white: #fff;
  --red-light: #f8d7da;
  --red-dark: #842029;
  --green-light: #d1e7dd;
  --green-dark: #0f5132;

  --borderRadius: 0.25rem;
  --letterSpacing: 1px;
  --transition: 0.3s ease-in-out all;
  --max-width: 1120px;
  --fixed-width: 600px;
  --view-width: 90vw;
  --shadow-1: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  --shadow-2: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
  --shadow-3: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
  --shadow-4: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

* {
  box-sizing: border-box;
}

body,
p,
h1,
h2,
li,
ul {
  padding: 0px;
  margin: 0px;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 1rem;
}

img {
  max-width: 100%;
  display: block;
}

.btn {
  cursor: pointer;
  border: transparent;
  border-radius: var(--borderRadius);
  padding: 0.375rem 0.75rem;
  font-family: inherit;
  text-transform: capitalize;
  letter-spacing: var(--letterSpacing);
  background-color: var(--primary-200);
  color: var(--primary-500);
}

.container {
  padding: 1rem;
  max-width: var(--max-width);
  margin: 0 auto;
  @media screen and (min-width: 768px) {
    padding: 1.5rem 2rem;
  }
}

.v-enter-active,
.v-leave-active{
  transition: opacity .3s;
}

.v-enter,
.v-leave-to{
  opacity: 0;
}

#app {
  main {
    display: flex;
    flex-direction: column;
    min-height: 100vh;

    .meals, .mealsSearch {
      flex: 1;
    }
  }
}
</style>
