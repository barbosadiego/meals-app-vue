<template>
  <div id="app">
    <TopBar />
  </div>
</template>

<script>
import TopBar from '@/components/TopBar.vue'

export default {
  name: 'App',
  components: {
    TopBar,
  },
};
</script>

<style lang="scss">
:root {
  --primary-100: #e6f0ff;
  --primary-200: #b4d3fe;
  --primary-300: #82b6fd;
  --primary-400: #5098fc;
  --primary-500: #03449d;
  --primary-600: #034caf;
  --primary-700: #02367d;
  --primary-800: #01214b;
  --primary-900: #000b19;
  --grey-50: #f8fafc;
  --grey-100: #f1f5f9;
  --grey-200: #e2e8f0;
  --grey-300: #cbd5e1;
  --grey-400: #94a3b8;
  --grey-500: #64748b;
  --grey-600: #475569;
  --grey-700: #334155;
  --grey-800: #1e293b;
  --grey-900: #0f172a;
  --black: #222;
  --white: #fff;
  --red-light: #f8d7da;
  --red-dark: #842029;
  --green-light: #d1e7dd;
  --green-dark: #0f5132;
}
#app {
}
</style>
