<template>
  <aside class="contacts-section">
    <h2>All Contacts</h2>

    <div class="contacts-list">
      <button
        v-for="(contact, index) in contacts"
        :key="index"
        class="contact-item"
        :class="{ selected: selectedIndex === index }"
        @click="$emit('select-contact', index)"
      >
        {{ contact.name }}
      </button>
    </div>

    <button class="main-button" @click="$emit('add-contact')">
      Add
    </button>
  </aside>
</template>

<script>
export default {
  name: 'ContactList',

  props: {
    contacts: {
      type: Array,
      required: true,
    },
    selectedIndex: {
      type: Number,
      default: null,
    },
  },

  emits: ['select-contact', 'add-contact'],
}
</script>