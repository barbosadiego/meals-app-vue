<template>
  <section class="favorites">
    <div class="container">
      <h1>favorites</h1>
    </div>
  </section>
</template>

<script>
export default {
  name: 'FavoritesComponent',
};
</script>

<style lang="scss" scoped>
@import '@/Functions';

.favorites {
  background-color: var(--black);

  h1{
    font-weight: 400;
    font-size: rem(20);
    text-transform: capitalize;
    color: var(--white);
    letter-spacing: var(--letterSpacing);
  }
}
</style>
