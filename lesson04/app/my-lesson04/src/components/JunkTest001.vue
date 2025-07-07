<template>
  <div>hello! {{ props.name }}</div>
</template>

<script setup>
import {defineProps} from 'vue';

  const props = defineProps({
    name: {
      type: String,
      required: true,
    }
  })


</script>