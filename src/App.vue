<template>
  <div :class="$style.btnWrap">
    <ElButton
      label="Open modal"
      class="btn-primary"
      :class="$style.btnModal"
      @click="onClickOpenModal"
    />

    <ElButton
      label="Open modal users"
      class="btn-primary"
      @click="onClickOpenModalUsers"
    />
  </div>

  <User v-for="user in users" :key="user.id" :user="user" />

  <Modal ref="modal">slot</Modal>
  <ModalUsers ref="modalUsers" :options="usersOption" />
</template>

<script setup lang="ts">
import Modal from "@components/Modal.vue"
import ModalUsers from "@components/ModalUsers.vue"
import ElButton from "@components/ElButton.vue"
import User from "@components/User.vue"
import { ref } from "vue"

interface IModal {
  show: () => Promise<Array<IUser>>
}

interface IUser {
  id: number
  value: string
}

const usersOption = [
  {
    id: 1,
    value: "John",
  },
  {
    id: 2,
    value: "Sam",
  },
]

const modal = ref<IModal>()
const modalUsers = ref<IModal>()
const users = ref<Array<IUser>>([])

const onClickOpenModal = async () => {
  const modalValue = await (modal.value as IModal).show()
}

const onClickOpenModalUsers = async () => {
  const modalValue = await (modalUsers.value as IModal).show()

  users.value = modalValue as Array<IUser>
}
</script>

<style lang="scss" module>
.btnWrap {
  margin-bottom: 20px;
}

.btnModal {
  margin-right: 20px;
}
</style>
