<template>
    <div class="right">
        <ul class="card-list">
            <li v-for="card in 12" :key="card">
                <card />
            </li>
        </ul>
    </div>
</template>

<script>
import card from './UI/card.vue'
    export default {
        components: { 
            card 
        },
        
    }
</script>

<style lang="scss" scoped>
.right {
  height: 1164px;
}

.card-list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
  list-style: none;
  padding: 0;
  margin: 0;

  @media (width <= 1440px) {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
  }
  @media (width <= 1000px) {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
  }
}
</style>

