<template>
  <table class="table">
    <thead>
    <tr>
        <th>#</th>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Username</th>
    </tr>
    </thead>
    <tbody>
     <tr v-for="employee in employees" :key="employee.id">
          <td>{{ employee.id }}</td>
        <td>{{ employee.firstName }}</td>
        <td>{{ employee.lastName }}</td>
        <td>{{ employee.userName }}</td>
        </tr>
    </tbody>
</table>
</template>

<script>
  export default {
    name: 'table',
    props: {
    employees: Array,
  },
  }
</script>

<style scoped></style>