<template>
    <div id="employee-table">
        <p v-if="employees.length < 1" class="empty-table">
            No Empty
        </p>
        <table>
            <thead>
                <tr>
                    <th>Employee name</th>
                    <th>Employee email</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="employee in employees" :key="employee.id" >
                    <td v-if="editing === employee.id">
                        <input type="text" v-model="employee.name">
                    </td>
                    <td v-else>{{employee.name}}</td>
                    <td v-if="editing===employee.id">
                        <input type="text" v-model="employee.email">
                    </td>
                    <td v-else>{{employee.email}}</td>
                    <td v-if="editing===employee.id">
                        <button @click="editEmployee(employee)">Seve</button>
                        <button class="muted-buttun" @click="cancelEdit(employee)">Cancel</button>
                        
                    </td>
                    <td v-else>
                        <button @click="editmode(employee)">Edit</button>
                        <button @click="$emit('delete:employee',employee.id)">Delete</button>
                    </td>
                </tr>
               
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    name: 'employee-table',
    data() {
        return{
            editing:null,
        }
    },
    methods: {
        editmode(employee) {
            this.cachedEmloyee = Object.assign({},employee)
            this.editing = employee.id
        },
        cancelEdit(employee){
            Object.assign(employee,this.cachedEmloyee)
            this.editing = null
        },
        editEmployee(employee) {
            if(employee.name === '' || employee.email === '') return
            this.$emit('edit:employee',employee.id,employee);
            this.editing = null
        }
    },
    props: {
        employees: Array
    }
}
</script>

<style scoped>
    table {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

table td, table th {
  border: 1px solid #ddd;
  padding: 8px;
}

table tr:nth-child(even){background-color: #f2f2f2;}

table tr:hover {background-color: #ddd;}

table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #4CAF50;
  color: white;
}
.empty-table {
    font-weight: bold;
    font-size: 1.3rem;
    background: yellow;
    color: black;
    padding: .5rem 1rem;
}
</style>