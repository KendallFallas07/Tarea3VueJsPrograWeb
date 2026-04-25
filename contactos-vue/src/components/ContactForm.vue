<template>
  <section class="form-section">
    <div class="form-group">
      <label>Name:</label>
      <input v-model="localForm.name" type="text" />
    </div>

    <div class="form-group">
      <label>Work:</label>
      <input v-model="localForm.work" type="text" />
    </div>

    <div class="form-group">
      <label>Mobile:</label>
      <input v-model="localForm.mobile" type="text" />
    </div>

    <div class="form-group">
      <label>Email:</label>
      <input v-model="localForm.email" type="email" />
    </div>

    <div class="form-group">
      <label>Address:</label>
      <textarea v-model="localForm.address"></textarea>
    </div>

    <div class="actions">
      <button class="delete-button" @click="$emit('delete-contact')">
        Delete
      </button>

      <button class="save-button" @click="$emit('save-contact', localForm)">
        Save
      </button>
    </div>

    <p v-if="message" class="message">
      {{ message }}
    </p>
  </section>
</template>

<script>
export default {
  name: 'ContactForm',

  props: {
    form: {
      type: Object,
      required: true,
    },
    message: {
      type: String,
      default: '',
    },
  },

  emits: ['save-contact', 'delete-contact'],

  data() {
    return {
      localForm: { ...this.form },
    }
  },

  watch: {
    form: {
      deep: true,
      handler(newValue) {
        this.localForm = { ...newValue }
      },
    },
  },
}
</script>