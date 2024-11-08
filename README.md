<template>
  <v-textarea
    v-model="value"
    label="Enter a number"
    @input="onInput"
  ></v-textarea>
</template>

<script>
export default {
  data() {
    return {
      value: '',
    };
  },
  methods: {
    onInput() {
      // Remove non-numeric characters and allow one decimal point and negative sign
      let filteredValue = this.value.replace(/[^0-9.-]/g, '');

      // Limit to one decimal point
      const decimalIndex = filteredValue.indexOf('.');
      if (decimalIndex !== -1) {
        filteredValue = filteredValue.slice(0, decimalIndex + 1) + filteredValue.slice(decimalIndex + 1).replace(/\./g, '');
      }

      // Ensure only one negative sign, and it is at the beginning
      if (filteredValue.indexOf('-') > 0) {
        filteredValue = filteredValue.replace(/-/g, '').replace(/^/, '-');
      }

      // Limit the length to 8 characters
      if (filteredValue.length > 8) {
        filteredValue = filteredValue.slice(0, 8);
      }

      // Update the value
      this.value = filteredValue;
    },
  },
};
</script>
