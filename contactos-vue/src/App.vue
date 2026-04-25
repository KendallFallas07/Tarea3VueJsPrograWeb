<template>
  <main class="page">
    <section class="app-window">
      <header class="window-header">
        <div class="buttons">
          <span></span>
          <span></span>
          <span></span>
        </div>
        <h1>A Web Page - Contact Manager</h1>
      </header>

      <section class="content">
        <ContactList
          :contacts="contacts"
          :selected-index="selectedIndex"
          @select-contact="selectContact"
          @add-contact="addContact"
        />

        <ContactForm
          :form="form"
          :message="message"
          @save-contact="saveContact"
          @delete-contact="deleteContact"
        />
      </section>
    </section>
  </main>
</template>

<script>
import ContactList from './components/ContactList.vue'
import ContactForm from './components/ContactForm.vue'
import { initialContacts } from './data/contacts'
import './assets/styles.css'

export default {
  name: 'App',

  components: {
    ContactList,
    ContactForm,
  },

  data() {
    return {
      contacts: [...initialContacts],
      selectedIndex: null,
      form: this.emptyForm(),
      message: '',
    }
  },

  methods: {
    emptyForm() {
      return {
        name: '',
        work: '',
        mobile: '',
        email: '',
        address: '',
      }
    },

    selectContact(index) {
      this.selectedIndex = index
      this.form = { ...this.contacts[index] }
      this.message = ''
    },

    addContact() {
      this.selectedIndex = null
      this.form = this.emptyForm()
      this.message = 'Ingrese la información del nuevo contacto.'
    },

    saveContact(contactData) {
      if (contactData.name.trim() === '') {
        this.message = 'El campo name es obligatorio.'
        return
      }

      if (this.selectedIndex === null) {
        this.contacts.push({ ...contactData })
        this.selectedIndex = this.contacts.length - 1
        this.message = 'Contacto agregado correctamente.'
      } else {
        this.contacts[this.selectedIndex] = { ...contactData }
        this.message = 'Contacto actualizado correctamente.'
      }

      this.form = { ...contactData }
    },

    deleteContact() {
      if (this.selectedIndex === null) {
        this.message = 'Seleccione un contacto para eliminar.'
        return
      }

      this.contacts.splice(this.selectedIndex, 1)
      this.selectedIndex = null
      this.form = this.emptyForm()
      this.message = 'Contacto eliminado correctamente.'
    },
  },
}
</script>