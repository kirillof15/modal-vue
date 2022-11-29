<template>
  <div :class="$style.user">
    <span>{{ user.id }}. {{ user.value }}</span>
  </div>
</template>

<script lang="ts" setup>
interface Props {
  user: {
    id: number
    value: string
  }
}

const { user } = defineProps<Props>()
</script>

<style lang="scss" module>
.user {
  background-color: rgb(205 193 193 / 30%);
  margin-bottom: 20px;
  padding: 1.1rem;
  max-width: 200px;
  margin: 0 auto;
  margin-bottom: 20px;
  border-radius: 10px;
}
</style>
