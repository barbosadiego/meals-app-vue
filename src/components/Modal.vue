<template>
  <div class="modal">
    <div class="modal__info">
      <img
        class="modal__img"
        data-v-54776de0=""
        src="https://www.themealdb.com/images/media/meals/ursuup1487348423.jpg"
        alt="Beef Brisket Pot Roast"
      />
      <h1>Title</h1>
      <div class="modal__description">
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ex cupiditate
          quidem autem, alias ullam ipsum nesciunt eveniet omnis vel.
          Accusantium quisquam, vitae praesentium fugit sed obcaecati
          perspiciatis corrupti consequatur labore.
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalComponent',
};
</script>

<style lang="scss" scoped>
.modal {
  position: fixed;
  z-index: 10;
  top: 0;
  left: 0;
  width: 100%;
  min-height: 100vh;
  background-color: transparentize($color: #000000, $amount: 0.1);
  overflow-y: auto;
  display: flex;
  justify-content: center;

  &__info {
    max-width: 900px;
    margin: 0 auto;
    background-color: var(--white);
    display: grid;
    grid-template-columns: 1fr;
    gap: 2rem;
    margin: 1rem;
    padding: 1.3rem;
    // border-radius: var(--borderRadius);
    @media screen and (min-width: 768px) {
      background-color: unset;
      background-image: linear-gradient(90deg, rgba(0, 0, 0, 0) 30%, white 30%);
      grid-template-columns: 250px 1fr;
      grid-template-rows: 300px 40px 1fr;
      margin: 3rem;
      padding: 1rem;
    }

    h1{
      // align-self: end;
      @media screen and (min-width:768px) {
        grid-column: 2/3;
      }
    }
    
  }

  &__img {
    border-radius: var(--borderRadius);
    @media screen and (min-width: 768px) {
      grid-column: 1/-1;
      height: 300px;
      width: 100%;
      object-fit: cover;
      object-position: top left;
    }
  }

  &__description {
    @media screen and (min-width: 768px) {
      grid-column: 2/3;
    }
  }
}
</style>
