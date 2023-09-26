<script setup>
import { defineProps, computed } from 'vue';

const props = defineProps({
  members: Array,
});

const typingText = computed(() => {
  const names = props.members.filter((member) => member.isTyping).map((member) => member.name);

  if (names.length === 0) {
    return '';
  }

  if (names.length === 1) {
    return `${names[0]} is typing`;
  }

  return `${names.slice(0, -1).join(', ')} and ${names.slice(-1)} are typing`;
});
</script>

<template>
  <div class="typingIndicator">
    <p>{{ typingText }}</p>
  </div>
</template>