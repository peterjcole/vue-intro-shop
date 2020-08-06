<template>
<div>
  <p>Details:</p>
  <ul>
    <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
  </ul>
  </div>
</template>

<script>
export default {
  props: {
    details: {
      type: [String],
      required: true
    }
  }
}
</script>