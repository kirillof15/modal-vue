<template>
  <button class="btn" :disabled="disabled" @click="onClick">{{ label }}</button>
</template>

<script lang="ts">
enum Emit {
  Click = "click",
}
</script>

<script setup lang="ts">
import { withDefaults } from "vue"

interface Props {
  label?: string
  disabled?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  disabled: false,
})

const emit = defineEmits([Emit.Click])

const onClick = () => emit(Emit.Click)
</script>

<style lang="scss" scoped>
.btn {
  &:disabled {
    background-color: rgba(163, 162, 162, 0.455);
    opacity: 1;
    cursor: no-drop;
  }
}
</style>
