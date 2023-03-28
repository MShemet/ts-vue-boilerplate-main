<script lang="ts" setup>
import { ref } from "vue";

import type Emoji from "@/types/Emoji";

import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";

const text = ref("");
const emoji = ref<Emoji | null>(null);
</script>
<template>
  <form class="entry-form" @submit.prevent>
    <textarea
      v-model="text"
      placeholder="New Journal Entry for danielkelly_io"
    ></textarea>

    <EmojiField v-model="emoji" />

    <div class="entry-form-footer">
      <span>0 / 280</span>
      <button>Remember <component :is="ArrowCircleRight" width="20" /></button>
    </div>
  </form>
</template>
