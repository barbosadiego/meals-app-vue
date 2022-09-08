<template>
  <div class="message">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: 'SystemMessage',
  props:{
    msg: String,
  }
}
</script>

<style lang="scss" scoped>
@import '@/Functions';

.message{
  position: fixed;
  background-color: lightgreen;
  z-index: 20;
  top: 10vh;
  left: 50%;
  transform: translateX(-50%);
  width: 90%;
  padding: 1rem;
  border-radius: var(--borderRadius);
  color: var(--green-dark);
  // box-shadow: var(--shadow-2);
  box-shadow: 0px 0px 0px 2px var(--green-dark);
  //tablet and desktop
  @media screen and (min-width: 768px) {
    width: unset;
  }
  
  p{
    font-size: rem(18);
    text-align: center;
  }
}
</style>