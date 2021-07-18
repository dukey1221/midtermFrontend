<template>

  <div>
    <NavBar />
    <EditContactModal :contact="selectedContact" />
    <DeleteContactModal :contact="selectedContact" @onDeleted="getAll" />
    <div class="container">
      <h1>
        Contacts
        <contactEntryModal class="float-right" @onAdd="getAll" />
      </h1>
      <table class="table table-bordered tabled-striped">
        <thead>
          <tr class="bg-info text-white">
            <th>Name</th>
            <th>Email</th>
            <th>Phone</th>
            <th>Address</th>
            <th>Job</th>
            <th>&nbsp;</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="contact in contacts" :key="contact.id">
            <td>{{contact.name}}</td>
            <td>{{contact.email}}</td>
            <td>{{contact.phone}}</td>
            <td>{{contact.address}}</td>
            <td>{{contact.job}}</td>
            <td>
              <b-button @click="onEdit(contact)" variant="info" size="sm">
                Edit
              </b-button>
              <b-button @click="onDelete(contact)" variant="danger" size="sm">
                Delete
              </b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>

</template>

<script>
export default {
  data() {
    return {
      contacts: [],
      selectedContact: {}
    }
  },
  methods: {
    async getAll() {
      await this.$axios.get('/api/contacts')
      .then((res)=>{
        if(res.status==202){
          this.contacts = res.data
        };
      })
    },
    onEdit(selectedContact) {
      this.selectedContact = selectedContact
      this.$bvModal.show('editContactModal')
    },
    onDelete(selectedContact) {
      this.selectedContact = selectedContact
      this.$bvModal.show('deleteContactModal')
    }
  },
  created() {
    this.getAll()
  }
}

</script>

<style>

</style>
