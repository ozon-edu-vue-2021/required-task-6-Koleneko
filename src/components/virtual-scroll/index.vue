<template>
  <div>
    <RecycleScroller
        :class="$style.scroller"
        :items="rows"
        :item-size="55"
        :buffer="10"
        page-mode
        key-field="id"
        v-slot="{ item }"
    >
      <Item :item="item"/>
    </RecycleScroller>
  </div>
</template>

<script>
import Item from './item';

export default {
  name: 'VirtualScrollWrapper',
  components: {Item},
  async created() {
    const res = await fetch(`https://jsonplaceholder.typicode.com/comments`);
    this.rows = await res.json();
  },
  data() {
    return {
      rows: [],
      rendered: false
    };
  }

};
</script>

<style module>
.scroller {
  text-align: left;
  margin: 24px;
}
</style>
