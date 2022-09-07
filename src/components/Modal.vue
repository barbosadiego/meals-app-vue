<template>
  <div class="modal" @click="handleClick">
    <div class="modal__info">
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
export default {
  name: 'ModalComponent',
  props: {
    idMeal: String,
  },
  data() {
    return {
      mealData: [],
      ingredients: [],
      measures: [],
      instructions: [],
    };
  },
  methods: {
    async getMealData() {
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
      }
    },
    ingredientsAndMeasures() {
      const size = this.ingredients.length - 1;
      for (let i = 0; i <= size; i++) {
        this.instructions.push(`${this.ingredients[i]} - ${this.measures[i]}`);
      }
    },
    handleClick({ target, currentTarget }) {
      // console.log(target);
      // console.log(currentTarget);
      target === currentTarget ? this.$emit('close') : false;
    },
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
    grid-template-columns: 1fr;
    gap: 2rem;
    margin: 1rem;
    padding: 1.3rem;
    // padding-top: 2rem;
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
      @media screen and (min-width: 768px) {
        grid-column: 2/3;
        // grid-row: 1;
        align-self: start;
        justify-self: end;
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
