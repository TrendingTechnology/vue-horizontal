<template>
  <div>
    <vue-horizontal ref="normal" class="normal">
      <section v-for="item in items" :key="item.i">
        <div class="header">
          <h6>{{ item.i }}</h6>
          <h3>{{ item.title }}</h3>
        </div>
        <p>{{ item.content }}</p>
      </section>
    </vue-horizontal>

    <div class="padded">
      <vue-horizontal ref="padded">
        <section v-for="item in items" :key="item.i">
          <div class="header">
            <h6>{{ item.i }}</h6>
            <h4>{{ item.title }}</h4>
          </div>
          <p>{{ item.content }}</p>
        </section>
      </vue-horizontal>
    </div>

    <div class="buttons">
      <button @click="goIndex(i)" v-for="i in [0,1,2,3,4,10,19,20,100,-1]" :key="i" :class="`btn-${i}`">
        Go {{ i }}
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import VueHorizontal from '@/vue-horizontal.vue';
import {Lorem} from './utils'

export default Vue.extend({
  components: {
    VueHorizontal
  },
  data() {
    const lorem = Lorem("scroll-to-index")
    return {
      items: [...Array(20).keys()].map((i) => {
        return {
          i,
          title: lorem.generateWords(2),
          content: lorem.generateSentences(1),
        };
      }),
    }
  },
  methods: {
    goIndex(index: number) {
      const normal = this.$refs.normal as any
      const padded = this.$refs.padded as any
      normal.scrollToIndex(index)
      padded.scrollToIndex(index)
    }
  }
});
</script>

<style scoped>
section {
  padding: 16px 24px;
  border-radius: 4px;
  background: #f5f5f5;
  margin-right: 24px;
  box-sizing: border-box;
  width: calc((100% - (3 * 24px)) / 4);
}

.header {
  display: flex;
}

.header h6 {
  background: #0000db;
  font-size: 14px;
  color: white;
  width: 24px;
  height: 24px;
  text-align: center;
  line-height: 24px;
  border-radius: 12px;
  margin-right: 12px;
  flex-shrink: 0;
}

button {
  margin-right: 12px;
}

.padded {
  padding: 0 240px;
}
</style>
