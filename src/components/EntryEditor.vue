<script lang="ts" setup>
import { ref, computed, onMounted, inject } from "vue";

import type Emoji from "@/types/Emoji";
import type Entry from "@/types/Entry";

import { userInjectionKey } from "@/injectionKeys";
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";

const body = ref("");
const emoji = ref<Emoji | null>(null);

const user = inject(userInjectionKey);

const charCount = computed<number>(() => body.value.length);
const maxChars = 280;

const textarea = ref<HTMLTextAreaElement | null>(null);

onMounted(() => {
  textarea.value?.focus();
});

const emit = defineEmits<{
  (e: "create", entry: Entry): void;
}>();

const handleTextInput = (e: Event) => {
  const textarea = e.target as HTMLTextAreaElement;

  if (textarea.value.length <= maxChars) {
    body.value = textarea.value;
  } else {
    body.value = textarea.value = textarea.value.substring(0, maxChars);
  }
};

const handleSubmit = () => {
  emit("create", {
    body: body.value,
    emoji: emoji.value,
    createdAt: new Date(),
    userId: 1,
    id: Math.random(),
  });

  body.value = "";
  emoji.value = null;
};
</script>

<template>
  <form class="entry-form" @submit.prevent="handleSubmit">
    <textarea
      ref="textarea"
      :value="body"
      :placeholder="`New Journal Entry for ${user?.username ?? 'ananymous'}}`"
      @keyup="handleTextInput"
    ></textarea>

    <EmojiField v-model="emoji" />

    <div class="entry-form-footer">
      <span>{{ charCount }} / {{ maxChars }}</span>
      <button>Remember <component :is="ArrowCircleRight" width="20" /></button>
    </div>
  </form>
</template>
