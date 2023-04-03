<script lang="ts" setup>
import DateDisplay from "./DateDisplay.vue";
import UseEmojis from "@/composables/UseEmojis";
import type Entry from "@/types/Entry";

const { findEmoji } = UseEmojis();

const props = defineProps<{
  entry: Entry;
}>();
</script>

<template>
  <div class="entry-card">
    <div class="entry-card-body">
      <component width="75" :is="findEmoji(props.entry.emoji)"></component>
      <div class="entry-text">{{ props.entry.body }}</div>
    </div>
    <div class="entry-footer">
      <DateDisplay :date="props.entry.createdAt" class="mr-2" />
      |
      <span class="ml-2">danielkelly_io</span>
    </div>
  </div>
</template>
