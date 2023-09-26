<script setup>
const props = defineProps({
  id: String,
  clientData: Object,
  isMe: Boolean,
});
</script>

<template>
  <div :key="id" class="member">
    <div class="avatar" :style="{ backgroundColor: clientData.color }" />
    <div class="username">{{ clientData.username }} {{ isMe ? ' (you)' : '' }}</div>
  </div>
</template>
