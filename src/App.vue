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
            <iframe
              v-else-if="isReddVid(pic)"
              id="reddit-embed"
              :src="pic"
              sandbox="allow-scripts allow-same-origin allow-popups"
              style="border: none;"
              height="500"
              width="500"
              scrolling="no"
            ></iframe>
            <img
              v-else-if="isRedditLink(pic)"
              src="./assets/reddit-logo.png"
              class="pic-img"
            />
            <div
              v-else-if="isGfycat(pic)"
              style="position:relative; padding-bottom:calc(100.00% + 44px)"
            >
              <iframe
                :src="pic"
                frameborder="0"
                scrolling="no"
                width="100%"
                height="100%"
                style="position:absolute;top:0;left:0;"
                allowfullscreen
              >
              </iframe>
            </div>
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
    },
    isGfycat(url: string): boolean {
      const lower = url.toLowerCase();
      return lower.includes("gfycat");
    },
    isReddVid(url: string): boolean {
      const lower = url.toLowerCase();
      return lower.includes("redditmedia");
    }
  }
});
</script>

<style lang="scss" src="./styles/App.scss"></style>
