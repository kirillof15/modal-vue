<template>
  <Teleport to="#modal">
    <transition name="modal" mode="out-in" appear>
      <div v-if="isShowModal" class="modal" @click.self="onClickModal">
        <div class="modal__container" :style="{ width: getWidth }">
          <div class="modal__header">
            <button class="modal__close-btn" @click="close">x</button>
          </div>

          <slot />

          <div class="modal__footer">
            <ElButton
              :label="labelCancel"
              class="btn-secondary"
              @click="close"
            />
          </div>
        </div>
      </div>
    </transition>
  </Teleport>
</template>

<script setup lang="ts">
import ElButton from "@components/ElButton.vue"
import { ref, withDefaults, computed } from "vue"

interface Props {
  labelOk?: string
  labelCancel?: string
  width?: number
}

const props = withDefaults(defineProps<Props>(), {
  labelOk: "Select",
  labelCancel: "Cancel",
  width: 500,
})

const isShowModal = ref(false)
const getWidth = computed(() => `${props.width}px`)

const show = async () => {
  isShowModal.value = true
}

const close = () => {
  isShowModal.value = false
}

const onClickModal = () => {
  close()
}

defineExpose({
  show,
  close,
})
</script>
