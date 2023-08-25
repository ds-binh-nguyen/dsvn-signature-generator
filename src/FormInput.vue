<template>
    <div>
      <label>{{ label }}</label>
      <input class="input" :value="value" @input="$emit('update:value', $event.target.value)" />
    </div>
</template>
  
<script>
  export default {
    props: {
      label: String,
      value: String,
    },
  };
</script>
  
<style>
  /* CSS cho component FormInput */
  .label {
    font-weight: bold;
  }
  
  .input {
    width: 100%;
    margin-bottom: 10px;
  }
</style>
  