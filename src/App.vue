<template>
  <div class="wrapper">
    <header>
      <header-block />
    </header>
    <main>
      <left-coll />
      <right-block />
    </main>
  </div>
</template>

<script setup>
import headerBlock from './components/header.vue'
import leftColl from './components/left-coll.vue';
import rightBlock from './components/right-block.vue';
</script>

<style lang="scss">

  .wrapper {
      padding: 0 100px 36px;
      display: flex;
      flex-direction: column;

      @media (width <= 1440px) {
          padding: 0 50px 36px;
      }
      @media (width <= 1000px) {
          padding: 0 16px;
      }
  }

  .btn {
    width: 75px;
    height: 40px;
  }

  main {
    display: flex;
    align-items: flex-start;
    gap: 36px;
    
    height: 1164px;
  }
</style>