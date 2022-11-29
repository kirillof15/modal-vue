<template>
  <transition name="modal" mode="out-in" appear>
    <div v-if="isShowModal" class="modal" @click.self="onClickModal">
      <div class="modal__container" :style="{ width: getWidth }">
        <div class="modal__header">
          <button class="modal__close-btn" @click="close">x</button>
        </div>

        <VueMultiselect
          v-model="users"
          track-by="id"
          label="value"
          placeholder="Select one"
          :options="options"
          :searchable="false"
          multiple
          :class="$style.user"
        />

        <slot />

        <div class="modal__footer">
          <ElButton
            :label="labelOk"
            :disabled="isDisabledBtnOk"
            class="btn-primary"
            @click="onClickBtnOk"
          />

          <ElButton :label="labelCancel" class="btn-secondary" @click="close" />
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup lang="ts">
import ElButton from "@components/ElButton.vue"
import VueMultiselect from "vue-multiselect/src/Multiselect.vue"
import { ref, withDefaults, computed } from "vue"

interface Props {
  labelOk?: string
  labelCancel?: string
  width?: number
  options: Array<unknown>
}

const props = withDefaults(defineProps<Props>(), {
  labelOk: "Select",
  labelCancel: "Cancel",
  width: 500,
})

const isShowModal = ref(false)
const users = ref([])
const getWidth = computed(() => `${props.width}px`)
const isDisabledBtnOk = computed(() => users.value.length === 0)
let promise: Function

const show = async () => {
  isShowModal.value = true

  const value = await new Promise((resolve) => (promise = resolve))

  isShowModal.value = false
  unsetUsers()

  return value
}

const onClickBtnOk = () => promise(users.value)

const close = () => {
  isShowModal.value = false
  unsetUsers()
}

const onClickModal = () => {
  close()
}

const unsetUsers = () => (users.value = [])

defineExpose({
  show,
  close,
})
</script>

<style lang="scss" module>
.user {
  margin-bottom: 20px;
}
</style>
