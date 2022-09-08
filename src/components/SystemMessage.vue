<template>
  <div class="message" :class="{'alert' : msg.alert}">
    <p>{{ msg.message }}</p>
  </div>
</template>

<script>
export default {
  name: 'SystemMessage',
  props:{
    msg: Object,
  },
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
  box-shadow: 0px 0px 0px 2px var(--green-dark);
  &.alert{
    background-color: var(--red-light);
    color: var(--red-dark);
    box-shadow: 0px 0px 0px 2px var(--red-dark);
  }
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