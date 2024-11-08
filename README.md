<template>
  <v-textarea
    v-model="value"
    label="Enter a number"
    @input="onInput"
  ></v-textarea>
</template>

<script setup>
import { ref } from 'vue';

// Declare a reactive variable `value` to bind to the v-textarea
const value = ref('');

// Handle the input event to filter the value and limit the input to 8 characters
const onInput = (event) => {
  // Get the current value from the event
  let inputValue = event.target.value;

  // Remove non-numeric characters
  inputValue = inputValue.replace(/[^0-9]/g, '');

  // Limit to 8 characters
  if (inputValue.length > 8) {
    inputValue = inputValue.slice(0, 8);
  }

  // Update the reactive `value`
  value.value = inputValue;
};
</script>
