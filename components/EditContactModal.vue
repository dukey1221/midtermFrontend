<template>
  <div>

    <b-modal id="editContactModal" title="Contact Entry" ok-title="Save Contact" @ok="onSubmit">
      <form action="#">
        <b-form-group
          label="Name"
          label-for="name"
        >
          <b-form-input id="name" v-model="contact.name" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Email"
          label-for="email"
        >
          <b-form-input id="email" v-model="contact.email" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Phone"
          label-for="phone"
        >
          <b-form-input id="phone" v-model="contact.phone" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Address"
          label-for="address"
        >
          <b-form-input id="address" v-model="contact.address" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Job"
          label-for="job"
        >
          <b-form-select v-model="contact.job" :options="jobs"></b-form-select>
        </b-form-group>

      </form>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    contact: {}
  },
  data() {
    return {
      jobs: [
        {value: 'developer', text: 'Developer'},
        {value: 'programmer', text: 'Programmer'},
      ]
    }
  },
  methods: {
    async onSubmit() {
      this.$axios.put('/api/contacts/' + this.contact.id, this.contact)
      .then((res)=>{
        if(res.status==202) {
          alert('Update successful!')
        }
      })
      .catch((err)=>{
        alert(err.message)
      })
    }
  }
}
</script>
