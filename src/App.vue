<script setup lang="ts">
import { reactive } from "vue";

import type User from "@/types/User";

import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "@/components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";

const user: User = reactive({
  id: 1,
  username: "test_user",
  settings: [],
});
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor />
    <ul>
      <li>
        <EntryCard />
      </li>
    </ul>
  </main>
</template>
