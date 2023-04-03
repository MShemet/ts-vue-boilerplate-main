<script lang="ts" setup>
import { inject } from "vue";

import type Entry from "@/types/Entry";

import { userInjectionKey } from "@/injectionKeys";
import UseEmojis from "@/composables/UseEmojis";

import DateDisplay from "./DateDisplay.vue";

const { findEmoji } = UseEmojis();

const props = defineProps<{
  entry: Entry;
}>();

const user = inject(userInjectionKey);
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
      <span class="ml-2">{{ user?.username ?? "ananymous" }}</span>
    </div>
  </div>
</template>
