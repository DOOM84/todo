<template>
    <div class="app-component">
        <table class="table">
            <thead>
            <tr>
                <th>Id</th>
                <th>Task Title</th>
                <th>Priority</th>
                <th>Action</th>
            </tr>
            </thead>
            <tbody>

            <task-component v-for="task in tasks" :key="task.id" :task="task"></task-component>

            <tr>
                <td colspan="2">
                    <input v-model="task.title" type="text" id="task" class="form-control">
                </td>
                <td>
                    <select v-model="task.priority" id="select" class="form-control">
                        <option>Low</option>
                        <option>Medium</option>
                        <option>High</option>
                    </select>
                </td>
                <td>
                    <button @click="store" class="btn btn-primary">ADD</button>
                </td>

            </tr>

            </tbody>

        </table>

    </div>
    
</template>

<script>
    import TaskComponent from './Task';
    export default {
        data(){
            return{

                tasks: [],
                task: {
                    title: '',
                    priority: ''
                },

                message: 'Hello FROM HERE....'

            }
        },

        methods:{

            getTasks(){
                window.axios.get('/api/tasks').then(({data})=>{
                    data.forEach(task=>{
                       this.tasks.push(task)
                    });
                });
            },
            store(){

            }

        },

        created(){
           this.getTasks();
        },
        components: {TaskComponent}
    }
</script>

<style scoped>

</style>