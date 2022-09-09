<template>
  <div class="modal" @click="handleClick">
    <Loading v-if="isLoading" />

    <div v-else class="modal__info">
      <button class="like" @click="addItem(mealData[0])">
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
      <button class="close-btn" @click="$emit('close')">close</button>
      <img
        class="modal__img"
        data-v-54776de0=""
        :src="mealData[0].strMealThumb"
        :alt="mealData[0].strMeal"
      />
      <div class="modal__description">
        <h1>{{ mealData[0].strMeal }}</h1>
        <h2>Cooking instructions:</h2>
        <p>{{ mealData[0].strInstructions }}</p>
        <h3>Ingredients and measures</h3>
        <div class="modal__measures">
          <p v-for="(item, index) in instructions" :key="index">
            {{ item }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loading from '@/components/Loading.vue';

export default {
  name: 'ModalComponent',
  components: {
    Loading,
  },
  props: {
    idMeal: String,
  },
  data() {
    return {
      mealData: [],
      ingredients: [],
      measures: [],
      instructions: [],
      isLoading: true,
    };
  },
  methods: {
    async getMealData() {
      this.isLoading = true;
      try {
        const data = await fetch(
          `https://www.themealdb.com/api/json/v1/1/lookup.php?i=${this.idMeal}`,
        );
        const response = await data.json();
        if (data.ok) {
          this.mealData = response.meals;

          for (let i = 0; i <= 20; i++) {
            if (this.mealData[0][`strIngredient${i}`]) {
              this.ingredients.push(this.mealData[0][`strIngredient${i}`]);
            }
            if (this.mealData[0][`strMeasure${i}`]) {
              this.measures.push(this.mealData[0][`strMeasure${i}`]);
            }
          }

          this.ingredientsAndMeasures();
        }
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoading = false;
      }
    },
    ingredientsAndMeasures() {
      const size = this.ingredients.length - 1;
      for (let i = 0; i <= size; i++) {
        this.instructions.push(`${this.ingredients[i]} - ${this.measures[i]}`);
      }
    },
    handleClick({ target, currentTarget }) {
      return target === currentTarget ? this.$emit('close') : false;
    },
    addItem(id){
      const item = {
        idMeal: id.idMeal, 
        strMeal: id.strMeal, 
        strMealThumb: id.strMealThumb
      };
      this.$emit('addItem', item)
    }
  },
  created() {
    this.getMealData();
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions.scss';

.modal {
  position: fixed;
  z-index: 10;
  top: 0;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: transparentize($color: #000000, $amount: 0.1);
  overflow-y: auto;
  display: flex;
  justify-content: center;

  &__info {
    max-width: 900px;
    overflow-y: auto;
    margin: 0 auto;
    background-color: var(--white);
    display: grid;
    justify-items: start;
    grid-template-columns: repeat(2,1fr);
    gap: 2rem;
    margin: 1rem;
    padding: 1.3rem;
    @media screen and (min-width: 768px) {
      background-color: unset;
      background-image: linear-gradient(90deg, rgba(0, 0, 0, 0) 30%, white 30%);
      grid-template-columns: 250px 1fr;
      grid-template-rows: 30px 1fr;
      margin: 3rem;
      padding: 1rem 2rem;
    }
    @media screen and (min-width: 880px) {
      grid-template-columns: 320px 1fr;
    }

    .close-btn {
      cursor: pointer;
      border: none;
      text-transform: uppercase;
      background-color: var(--red-dark);
      color: var(--white);
      padding: 0.5rem 1rem;
      border-radius: var(--borderRadius);
      justify-self: end;
      grid-row: 1;
      @media screen and (min-width: 768px) {
        grid-column: 2/3;
      }
    }

    .like {
      position: relative;
      top: 0px;
      grid-row: 1;
      background-color: transparent;
      border: none;
      transition: .3s;
      &:active{
        transform: scale(1.9) rotate(-25deg);
        svg{
          fill: var(--red-dark);
        }
      }
      @media screen and (min-width: 768px) {
        position: relative;
        grid-column: 2/3;
        grid-row: 1;
        align-self: start;
        cursor: pointer;
      }
    }
  }

  &__measures {
    p {
      text-transform: capitalize;
    }
  }

  &__img {
    border-radius: var(--borderRadius);
    grid-column: 1/-1;
    @media screen and (min-width: 768px) {
      position: fixed;
      grid-column: 1/2;
      grid-row: 2;
      height: 300px;
      width: 250px;
      object-fit: cover;
      object-position: top left;
    }
    @media screen and (min-width: 880px) {
      width: 300px;
    }
  }

  &__description {
    grid-column: 1/-1;
    h1,
    h2,
    h3,
    p {
      margin-bottom: 1rem;
      line-height: 1.4;
    }

    h1 {
      font-size: rem(25);
      line-height: 1.2;
      @media screen and (min-width: 768px) {
        font-size: rem(40);
      }
    }

    @media screen and (min-width: 768px) {
      grid-column: 2/3;
    }
  }
}
</style>
