<template>
  <section class="meals">
    <Loading v-if="isLoading"/>
    <div v-else class="container meals__grid">
      <div class="meals__item" v-for="item in mealData" :key="item.idMeal">
        <img
          :src="item.strMealThumb"
          :alt="item.strMeal"
          @click="$emit('mealItem', item.idMeal)"
        />
        <div class="meals__description">
          <p>{{ item.strMeal }}</p>
          <button class="like" @click="$emit('addItem', item)">
            <svg
              stroke="currentColor"
              fill="#000000"
              stroke-width="0"
              viewBox="0 0 16 16"
              height="1.3rem"
              width="1.3rem"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M8.864.046C7.908-.193 7.02.53 6.956 1.466c-.072 1.051-.23 2.016-.428 2.59-.125.36-.479 1.013-1.04 1.639-.557.623-1.282 1.178-2.131 1.41C2.685 7.288 2 7.87 2 8.72v4.001c0 .845.682 1.464 1.448 1.545 1.07.114 1.564.415 2.068.723l.048.03c.272.165.578.348.97.484.397.136.861.217 1.466.217h3.5c.937 0 1.599-.477 1.934-1.064a1.86 1.86 0 0 0 .254-.912c0-.152-.023-.312-.077-.464.201-.263.38-.578.488-.901.11-.33.172-.762.004-1.149.069-.13.12-.269.159-.403.077-.27.113-.568.113-.857 0-.288-.036-.585-.113-.856a2.144 2.144 0 0 0-.138-.362 1.9 1.9 0 0 0 .234-1.734c-.206-.592-.682-1.1-1.2-1.272-.847-.282-1.803-.276-2.516-.211a9.84 9.84 0 0 0-.443.05 9.365 9.365 0 0 0-.062-4.509A1.38 1.38 0 0 0 9.125.111L8.864.046zM11.5 14.721H8c-.51 0-.863-.069-1.14-.164-.281-.097-.506-.228-.776-.393l-.04-.024c-.555-.339-1.198-.731-2.49-.868-.333-.036-.554-.29-.554-.55V8.72c0-.254.226-.543.62-.65 1.095-.3 1.977-.996 2.614-1.708.635-.71 1.064-1.475 1.238-1.978.243-.7.407-1.768.482-2.85.025-.362.36-.594.667-.518l.262.066c.16.04.258.143.288.255a8.34 8.34 0 0 1-.145 4.725.5.5 0 0 0 .595.644l.003-.001.014-.003.058-.014a8.908 8.908 0 0 1 1.036-.157c.663-.06 1.457-.054 2.11.164.175.058.45.3.57.65.107.308.087.67-.266 1.022l-.353.353.353.354c.043.043.105.141.154.315.048.167.075.37.075.581 0 .212-.027.414-.075.582-.05.174-.111.272-.154.315l-.353.353.353.354c.047.047.109.177.005.488a2.224 2.224 0 0 1-.505.805l-.353.353.353.354c.006.005.041.05.041.17a.866.866 0 0 1-.121.416c-.165.288-.503.56-1.066.56z"
              ></path>
            </svg>
          </button>
        </div>
      </div>
      <p v-if="isError">Ops, something was wrong...</p>
    </div>
  </section>
</template>

<script>
import Loading from '@/components/Loading.vue';

export default {
  name: 'MealsComponent',
  components:{
    Loading,
  },
  data() {
    return {
      mealData: [],
      isError: false,
      idMeal: null,
      isLoading: false,
    };
  },
  methods: {
    async getMeals() {
      this.isLoading = true;
      try {
        const data = await fetch(
          'https://www.themealdb.com/api/json/v1/1/filter.php?a=American',
        );
        const response = await data.json();
        if (response.meals) {
          this.mealData = response.meals;
        } else {
          console.log(data);
          this.isError = true;
        }
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoading = false;
      }
    },
  },
  mounted() {
    this.getMeals();
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions';

.meals {
  background-color: var(--grey-100);
  // padding-top: 2rem;
  position: relative;

  &__grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
    //tablet and desktop
    @media screen and (min-width: 768px) {
      grid-template-columns: repeat(3, 1fr);
      gap: 2rem;
    }
  }

  &__item {
    cursor: pointer;
    background-color: var(--white);
    border-radius: var(--borderRadius);
    overflow: hidden;
    position: relative;
    box-shadow: var(--shadow-3);
    height: 230px;
    img {
      transform: translateY(-20%);
    }
    @media screen and (min-width: 768px) {
      height: unset;
      img {
        transform: translateY(0%);
      }
    }
  }

  &__description {
    background-color: var(--white);
    position: absolute;
    bottom: 0px;
    width: 100%;
    border-bottom-left-radius: var(--borderRadius);
    border-bottom-right-radius: var(--borderRadius);
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;

    p {
      font-size: rem(16);
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
    }

    .like {
      cursor: pointer;
      transition: 0.3s;
      background-color: transparent;
      border: none;
      padding: 0px;
      margin: 0px;

      svg {
        transition: 0.3s;
      }

      &:hover {
        svg {
          fill: var(--red-dark);
        }
        @media screen and (min-width: 1025px) {
          transform: translateY(-5px);
        }
      }
    }
  }
}
</style>
