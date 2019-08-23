<template>
  <div id="app" class="small-container">
    <h1>Employee</h1>

    <employee-from @add:employee="addEmployee"/>
    <employee-table v-bind:employees="employees" 
    @delete:employee='deleteEmployee'
    @edit:employee="editEmployee"
    />
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable'
import EmployeeFrom from '@/components/EmployeeFrom' 
export default {
  name: 'App',
  components: {
    EmployeeTable,
    EmployeeFrom
  },
  data (){
    return {
      employees: [
        {
          id:1,
          name: 'jakkraphan',
          email: 'jakkraphan21544@gmail.com'
        },
        {
          id:2,
          name: 'jakkraphan2',
          email: 'jakkraphan21554@gmail.com'
        },
        {
          id:3,
          name: 'jakkraphan3',
          email: 'jakkraphan21546@gmail.com'
        }
      ]
    }
  },
  methods: {
    addEmployee(employee){
      const lastId =
      this.employees.length > 0 ? this.employees[this.employees.length -1].id : 0;

      const id = lastId +1;
      const newEmployee = {...employee,id};

      this.employees = [...this.employees, newEmployee]
      console.log(this.employees);
      
    },
    deleteEmployee (id) {
      this.employees = this.employees.filter(employees => employees.id !== id)
    },
    editEmployee (id,updatadEmployee) {
      this.employees = this.employees.map(employee => employee.id === id ? updatadEmployee : employee)
    }
  }
  
}
</script>

<style>
    button {
      background-color:green;
      border: 1px solid  green;
      padding: .8em;
      color:white;
    }
    button:hover,
    button:active,
    button:focus {
      background-color:green;
      border: 1px solid  green;
    }
  .small-container {
    max-width: 680;
  }
</style>
