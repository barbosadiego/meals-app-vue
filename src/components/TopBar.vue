<template>
  <header class="top-bar container">
    <form class="top-bar__search">
      <input
        type="text"
        name="meal"
        id="meal"
        v-model="meal"
        placeholder="Type your favorite meal"
      />
      <button
        class="btn top-bar__search-btn"
        type="submit"
        @click.prevent="handleSearch"
      >
        search
      </button>
    </form>
    <button class="btn top-bar__surprise-btn"
      @click="$emit('initSurprise')"
    >
      surprise me!
    </button>
  </header>
</template>

<script>
export default {
  name: 'TopBar',
  data() {
    return {
      meal: '',
    };
  },
  methods: {
    handleSearch() {
      console.log('search');
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions.scss';

.top-bar {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  width: 100%;

  &__search {
    input {
      padding: 0.375rem 0.75rem;
      border: 1px solid var(--primary-200);
      border-radius: var(--borderRadius);
      background-color: var(--primary-100);
      outline: none;
      transition: .3s;

      &::placeholder {
        color: var(--grey-400);
      }

      &:focus{
        box-shadow: 0px 0px 0px 2px var(--primary-200);
      }
    }
  }

  &__search-btn {
    margin-left: 8px;
    background-color: var(--primary-500);
    color: var(--white);
    transition: 0.3s;
    box-shadow: var(--shadow-1);

    &:hover {
      background-color: var(--primary-700);
    }
  }

  &__surprise-btn {
    transition: .3s;
    
    &:hover {
      background-color: var(--grey-800);
      color: var(--white);
    }
  }
}
</style>
