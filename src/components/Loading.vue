<template>
  <div class="loading">
    <div class="loading__icon"></div>
  </div>
</template>

<script>
export default {
  name: 'LoadingComponent',
}
</script>

<style lang="scss" scoped>
.loading{
  width: 100%;
  min-height: 100vh;
  background-color: transparentize($color: #000000, $amount: .4);
  position: absolute;
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;

  &__icon{
    display: block;
    width: 80px;
    height: 80px;
    background-color: transparent;
    border-radius: 50%;
    border: 10px solid var(--white);
    border-top-color: transparent;
    animation: rotation 1s ease infinite ;
  }

  @keyframes rotation {
    to{
      transform: rotate(360deg);
    }
  }
}
</style>