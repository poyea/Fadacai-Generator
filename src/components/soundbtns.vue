<template>
  <b-card title="所有聲音" sub-title>
    <hr />
    <div class="row">
      <div class="col-8 my-2">
        <b-form-input v-model="search" placeholder="搜索聲音..."></b-form-input>
      </div>
      <div class="col-4 my-2">
        <b-button variant="info" @click="random()">隨機3個</b-button>
      </div>
      <div class="col-12 my-2">
        <b-button
          class="m-1"
          v-for="(s, idx) in this.filtered"
          :key="idx"
          variant="success"
          @click="add(s.id)"
          >{{ s.name }}</b-button
        >
      </div>
    </div>
  </b-card>
</template>
<script>
import { eventBus } from "../main.js";
export default {
  name: "sounds",
  props: {
    sounds: Array
  },
  data() {
    let search = "";
    return {
      search
    };
  },
  methods: {
    add(id) {
      eventBus.$emit("addSound", id);
    },
    random() {
      for (let i = 0; i < 3; ++i)
        this.add(Math.floor(Math.random() * this.sounds.length));
    }
  },
  computed: {
    filtered() {
      return this.sounds.filter(s => {
        return s.name.includes(this.search);
      });
    }
  }
};
</script>
