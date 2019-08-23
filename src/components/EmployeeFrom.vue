<template>
    <div id="employee-from" >
        <form @submit.prevent="handleSubmit">
            <label >EmployeeName</label>
            <input 
            ref="first"
            type="text"
            :class="{  'has-error' : submitting && invalidName  }"
            v-model="employee.name" 
            @focus="clearStatus"
            @keypress="clearStatus"
           
            >
            <br>
            <label >EmployeeEmail</label>
            <input 
            :class="{  'has-error' : submitting && invalidEmail  }"
            v-model="employee.email" 
            type="text"
            @focus="clearStatus"
            >
            <br>
            <p v-if="error && submitting" class="error-massage">
                please fill out all required field

            </p>
            <p v-if="success && submitting" class="success-massage">
                employee successfully added
            </p>
            <button>Add Employee</button>
        </form>
    </div>
</template>
<script>
export default {
    name: 'employee-from',
    data(){
        return {
            submitting: false,
            error: false,
            success: false,


            employee: {
                name: '',
                email: '',
            }
        }
    },
    methods:{
        handleSubmit () {
            this.submitting = true
            this.clearStatus()

            if (this.invalidName || this.invalidEmail) {
                this.error = true
                return
            }
            
            this.$emit('add:employee',this.employee);
            this.$refs.first.focus();
            

            this.employee = {
                name: '',
                email: '',
                
            }
            this.error = false
            this.success = true
            this.submitting = true

            
            
        },
        clearStatus() {
                this.success = false
                this.error = false
            }
       
    },
    computed: {
        invalidName() {
            return this.employee.name === ''
            
        },
        invalidEmail() {
            return this.employee.email === ''
        }
    }
   
}
</script>
<style scoped>
    form {
        margin-bottom: 2rem;
    }
    input{
        margin-bottom: 2rem;
    }
    [class*='-masseage'] {
        font-weight: bold;
    }
    .error-massage {
        color: #d33c40
    }
    .success-massage {
        color: #32a95d
    }
</style>