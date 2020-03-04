<template>
  <div id="table">
    <p v-if="employees.length < 1" class="empty-table">No employees</p>
    <table v-else>
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

          <td v-if="editing == employee.id">
            <input type="text" v-model="employee.firstName" />
          </td>
          <td v-else>{{ employee.firstName }}</td>

          <td v-if="editing == employee.id">
            <input type="text" v-model="employee.lastName" />
          </td>
          <td v-else>{{ employee.lastName }}</td>

          <td v-if="editing == employee.id">
            <input type="text" v-model="employee.userName" />
          </td>
          <td v-else>{{ employee.userName }}</td>

          <td v-if="editing == employee.id">
            <button class="button primary" @click="editEmployee(employee)">Save</button>
            <button class="button" @click="editing = null">Cancel</button>
          </td>
          <td v-else>
            <button class="button success" @click="editMode(employee.id)">Edit</button>
            <button class="button alert" @click="$emit('delete:employee', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "table",
  props: {
    employees: Array
  },
  data() {
    return {
      editing: null
    };
  },
  methods: {
    editMode(id) {
      console.log(id)
      this.editing = id;
    },
    editEmployee(employee) {
      if (
        employee.firstName === "" ||
        employee.lastName === "" ||
        employee.userName === ""
      )
        return;
      this.$emit("edit:employee", employee.id, employee);
      this.editing = null;
    }
  }
};
</script>

<style scoped>
button {
  margin: 0 0.5rem 0 0;
}
</style>