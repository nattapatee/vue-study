<template>
  <div id="form">
    <form @submit.prevent="handleSubmit">
      <label>Employee Firstnmae</label>
      <input 
      type="text" 
      v-model="employee.firstName" 
      :class="{ 'has-error': submitting && invalidName }"
      @focus="clearStatus"
      @keypress="clearStatus"
     />
      <label>Employee Lastname</label>
      <input 
      type="text" 
      v-model="employee.lastName"
      :class="{ 'has-error': submitting && invalidLastname }"
      @focus="clearStatus"
      />
      <label>Employee Username</label>
      <input type="text" v-model="employee.userName"/>
      <br />
      <p v-if="error && submitting" class="error-message">
    ❗Please fill out all required fields
  </p>
  <p v-if="success" class="success-message">
    ✅ Employee successfully added
  </p>
      <button type="submit" class="button primary" >Add Employee</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'form',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        employee: {
          firstName: '',
          lastName: '',
          userName: ''
        },
      }
    },
  methods: {
    handleSubmit() {
         this.submitting = true
    this.clearStatus()

    if (this.invalidName || this.invalidLastname) {
      this.error = true
      return
    }

    this.$emit('add:employee', this.employee)
    this.employee = {
      firstName: '',
      lastName: '',
    }
    this.error = false
    this.success = true
    this.submitting = false
    },

  clearStatus() {
    this.success = false
    this.error = false
  }
  },
  computed: {
  invalidName() {
    return this.employee.firstName === ''
  },

  invalidLastname() {
    return this.employee.lastName === ''
  },
},
  }
</script>

<style scoped>
   form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>