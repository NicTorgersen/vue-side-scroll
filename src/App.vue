<script setup>
import { ref } from 'vue';
import SideScroll from '@/components/SideScroll.vue';

let itemRange = [...Array(14).keys()];

const items = ref(itemRange.map(key => {
    const index = key+1;
    return {
        url: `#test${index}`,
        innerHtml: `Kategori ${index}`,
    }
}))

</script>

<template>
    <div style="width: 350px">
        <SideScroll :items="items" />
    </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
