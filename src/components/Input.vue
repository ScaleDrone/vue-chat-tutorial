<script setup>
import { ref, onMounted, defineProps } from 'vue';
import TypingIndicator from 'typing-indicator';

const props = defineProps({
  onSendMessage: Function,
  onChangeTypingState: Function,
});

let typingIndicator = null;

const text = ref('');

onMounted(() => {
  if (typingIndicator === null) {
    typingIndicator = new TypingIndicator();
    typingIndicator.listen(props.onChangeTypingState);
  }
});

function onChange(e) {
  const textValue = e.target.value;
  typingIndicator.onChange(textValue);
  text.value = textValue;
}

function onSubmit() {
  props.onSendMessage(text.value);
  text.value = '';
}
</script>

<template>
  <div class="input">
    <form @submit.prevent="onSubmit">
      <input v-model="text" @input="onChange" />
      <button type="button" @click="onSubmit">Send</button>
    </form>
  </div>
</template>