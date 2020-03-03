<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee"/>

    <employee-table v-bind:employees="employees"/>
  </div>
</template>

<script>
  import EmployeeTable from '@/components/EmployeeTable.vue'
  import EmployeeForm from '@/components/EmployeeForm.vue'

  export default {
    name: 'app',
    components: {
      EmployeeTable,
      EmployeeForm,
    },
    data() {
      return {
      employees: [{
        id: 1,
        firstName: "Bill",
        lastName: "Gates",
        userName: "@billy"
      },{
        id: 2,
        firstName: "Steve",
        lastName: "Jobs",
        userName: "@stevy"
      },{
        id: 4,
        firstName: "Bill",
        lastName: "Gates",
        userName: "@billy"
      },{
        id: 5,
        firstName: "Larry",
        lastName: "Page",
        userName: "@larry"
      },{
        id: 6,
        firstName: "Banana",
        lastName: "Apple",
        userName: "@fruit"
      },]
    }},
    methods: {
  addEmployee(employee) {
    const lastId =
    this.employees.length > 0
      ? this.employees[this.employees.length - 1].id
      : 0;
  const id = lastId + 1;
  const newEmployee = { ...employee, id };

  this.employees = [...this.employees, newEmployee];
  }
}
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
    margin-left: 200px;
  }
</style>