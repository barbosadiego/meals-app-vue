<template>
  <section class="favorites" v-if="favorites.length > 0">
    <div class="container">
      <h1>favorites</h1>
      <div class="favorites__grid">
        <div class="favorites__meal"
          v-for="item in favorites"
          :key="item.idMeal"
        >
          <img
            class="favorites__icon"
            :src="item.strMealThumb"
            :alt="item.strMeal"
          />
          <button @click="$emit('removeItem', item)">Remove</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: 'FavoritesComponent',
  data() {
    return {
      favoritesArray: [],
    };
  },
  props:{
    favorites: Array,
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions';

.favorites {
  background-color: var(--black);

  h1 {
    font-weight: 400;
    font-size: rem(20);
    text-transform: capitalize;
    color: var(--white);
    letter-spacing: var(--letterSpacing);
    margin-bottom: 1rem;
  }

  &__grid {
    display: flex;
    gap: 1rem;
    overflow-x: auto;
    padding: 0.5rem;

    @media screen and (min-width: 768px) {
      &::-webkit-scrollbar {
        background-color: darken(#222, 20%);
        height: 7px;
        border-radius: 3px;
      }

      &::-webkit-scrollbar-thumb {
        background-color: lighten($color: #222, $amount: 20%);
        border-radius: 3px;
      }
    }
  }

  &__meal {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: center;
    font-size: rem(12);

    button {
      color: var(--white);
      background-color: transparent;
      border: none;
      cursor: pointer;
    }
  }

  &__icon {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    box-shadow: 0px 0px 0px 2px var(--black), 0px 0px 0px 5px var(--white);
    margin: 0px 0.5rem;
    position: relative;
  }
}
</style>
