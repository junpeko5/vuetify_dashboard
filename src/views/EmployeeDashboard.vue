<template>
  <div>
    <h1>Employee Dashboard</h1>
    <v-data-table
      :headers="headers"
      :items="employee"
      :items-per-page="5"
      class="elevation-1"
      @click:row="selectRow"
    ></v-data-table>
    <v-snackbar
      v-model="snackbar"
    >
      You have selected {{ selectedEmployee.name }},
      {{ selectedEmployee.title }}

      <template v-slot:action="{ attrs }">
        <v-btn
          color="pink"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
import employeeData from '../data/employee.json'
export default {
  name: 'employeeDashboard',
  data() {
    return {
      snackbar: false,
      selectedEmployee: {
        name: '',
        title: ''
      },
      headers: [
        { text: 'Id', value: 'id' },
        { text: 'Name', value: 'name'},
        { text: 'Title', value: 'title'},
        { text: 'Salary', value: 'salary'},
      ],
      employee: employeeData
    }
  },
  methods: {
    selectRow(event) {
      this.snackbar = true
      this.selectedEmployee.name = event.name
      this.selectedEmployee.title = event.title
    }
  }
}
</script>