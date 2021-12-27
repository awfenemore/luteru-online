<template>
  <v-app>
    <div class="heading-container">
      <h1 class="heading">Inspirations</h1>
      <div class="menu-container">
        <a
          class="menu-link"
          v-for="(item, i) in items"
          :key="i"
          :href="'#' + item.title"
          >{{ item.title }}</a
        >
      </div>
    </div>
    <div class="content-container">
      <div
        class="section"
        v-for="(item, i) in items"
        :key="i"
        :id="'#' + item.title"
      >
        <h3>{{ item.title }}</h3>
        <div class="section-links">
          <a
            class="pic-link"
            v-for="(pic, j) in item.pics"
            :key="j"
            :href="pic"
            target="_blank"
          >
            <img v-if="isImage(pic)" :src="pic" class="pic-img" />
            <img
              v-else-if="isRedditLink(pic)"
              src="./assets/reddit-logo.png"
              class="pic-img"
            />
            <h3 v-else>{{ pic }}</h3></a
          >
        </div>
      </div>
    </div>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
// @ts-ignore
import items from "./items";

export default Vue.extend({
  name: "App",
  data() {
    return {
      items: items
    };
  },
  methods: {
    isImage(url: string): boolean {
      const lower = url.toLowerCase();
      return lower.includes(".jpg") || lower.includes(".png");
    },
    isRedditLink(url: string): boolean {
      const lower = url.toLowerCase();
      return lower.includes("redd");
    }
  }
});
</script>

<style lang="scss" src="./styles/App.scss"></style>
