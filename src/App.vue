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

  --borderRadius: 0.25rem;
  --letterSpacing: 1px;
  --transition: 0.3s ease-in-out all;
  --max-width: 1120px;
  --fixed-width: 600px;
  --view-width: 90vw;
  --shadow-1: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  --shadow-2: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  --shadow-3: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  --shadow-4: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

*{
  box-sizing: border-box;
}

body, p, h1, h2, li, ul{
  padding: 0px;
  margin: 0px;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1rem;
}

.btn{
  cursor: pointer;
  border: transparent;
  border-radius: var(--borderRadius);
  padding: .375rem .75rem;
  font-family: inherit;
  text-transform: capitalize;
  letter-spacing: var(--letterSpacing);
  background-color: var(--primary-200);
  color: var(--primary-500);
}
</style>