<script setup>
import { ref, onMounted, defineProps } from 'vue';
import TypingIndicator from 'typing-indicator';

let typingIndicator = null;

const props = defineProps({
  onSendMessage: Function,
  onChangeTypingState: Function,
});

const text = ref('');

function onChange(e) {
  const textValue = e.target.value;
  typingIndicator.onChange(textValue);
  text.value = textValue;
}

function onSubmit() {
  props.onSendMessage(text.value);
  text.value = '';
}

onMounted(() => {
  if (typingIndicator === null) {
    typingIndicator = new TypingIndicator();
    typingIndicator.listen(props.onChangeTypingState);
  }
});
</script>

<template>
  <div class="input">
    <form @submit.prevent="onSubmit">
      <input v-model="text" @input="onChange" />
      <button type="button" @click="onSubmit">Send</button>
    </form>
  </div>
</template>