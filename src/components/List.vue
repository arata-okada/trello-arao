<template>
  <div class="list">
    <div class="listheader">
      <div class="top">
        <p class="list-title">{{ title }}</p>
        <p class="list-counter">total:{{ totalCardInList }}</p>
      </div>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <draggable group="cards" :list="cards" @end="$emit('change')">
      <Card
        v-for="(item, index) in cards"
        :key="item.id"
        :body="item.body"
        :cardIndex="index"
        :listIndex="listIndex"
      />
      <CardAdd :listIndex="listIndex" />
    </draggable>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import CardAdd from "./CardAdd";
import Card from "./Card";
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    cards: {
      type: Array,
      required: true,
    },
    listIndex: {
      type: Number,
      required: true,
    },
  },
  methods: {
    removeList() {
      if (confirm("本当にこのリストを削除しますか？")) {
        this.$store.dispatch("removelist", { listIndex: this.listIndex });
      }
    },
  },
  computed: {
    totalCardInList() {
      return this.cards.length;
    },
  },
  components: {
    CardAdd,
    Card,
    draggable,
  },
};
</script>
