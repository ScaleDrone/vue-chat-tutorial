<script setup>
import Member from './Member.vue';
import { defineProps } from 'vue';

const props = defineProps({
  members: Array,
  me: Object,
});
</script>

<template>
  <div class="members">
    <div class="membersCount">
      {{ members.length }} user{{ members.length === 1 ? '' : 's' }} online
    </div>
    <div class="membersList">
      <Member v-for="member in members" :key="member.id" :id="member.id" :client-data="member.clientData"
        :is-me="member.id === me.id" />
    </div>
  </div>
</template>