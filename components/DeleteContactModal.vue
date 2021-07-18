<template>
  <div>

    <b-modal id="deleteContactModal" title="Contact Entry" ok-title="Delete Contact" @ok="onDelete" ok-variant="danger">
      Are you sure about deleting this contact? <br>
      {{ contact.name }} {{ contact.email }}
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    contact: {}
  },
  methods: {
    async onDelete() {
      this.$axios.delete('/api/contacts/' + this.contact.id)
      .then((res)=>{
        if(res.status==202) {
          alert('Contact is deleted successfully!')
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>
