<template>
  <header>
    <div class="navbar">
      <div class="container">
        <div class="navbar-content">
          <Select @onSelected="handleSelected"></Select>
          <button @click="handleOpenModal" class="btn btnAdd" type="submit">
            <span class="for-large-screens">Добавить контакт</span
            ><span class="for-small-screens">Добавить</span>
          </button>
          <Modal v-if="isModalAddContact" :title="title"> <Form /> </Modal>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import Select from '@/components/UI/Select.vue'
import Modal from '@/components/UI/Modal.vue'
import Form from '@/components/contacs/ContactForm.vue'
import { useStore } from 'vuex'
import { ref, computed } from 'vue'
export default {
  components: {
    Select,
    Modal,
    Form
  },
  setup() {
    const title = 'Новый контакт'
    const store = useStore()
    const handleOpenModal = () => {
      store.dispatch('setIsModalAddContact', true)
    }
    const isModalAddContact = ref(
      computed(() => {
        return store.getters.getIsModalAddContact
      })
    )
    const handleSelected = selectedCategory => {
      store.dispatch('setDataSorted', selectedCategory)
    }
    return {
      title,
      isModalAddContact,
      handleOpenModal,
      handleSelected
    }
  }
}
</script>
