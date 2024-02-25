<template>
    <div>
        <h1>Job Posting Lists</h1>
        <table class="table table-hover table-bordered table-striped">
            <thead>
                <tr>
                    <th>JobName</th>
                    <th>JobDescription</th>
                    <th>Vacants</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in this.postings" :key="item.id">
                    <td>{{ item.job_name}}</td>
                    <td>{{ item.job_description}}</td>
                    <td>{{ item.vacants}}</td>
                    <td>
                        <button class="btn btn-primary btn-sm" data-bs-toggle="modal" data-bs-target="#exampleModal" data-bs-whatever="fds "><i class="bi-search"></i></button>
                        <button class="btn btn-danger btn-sm"><i class="bi-trash"></i></button>
                    </td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td>
                        <div class="form-group">
                            <input  type="text" class="form-control" placeholder="Input Job Name" v-model="form.job_name">
                        </div>
                    </td>
                    <td>
                        <div class="form-group">
                            <input type="text" class="form-control" placeholder="Input Job Decription" v-model="form.job_description">
                        </div>
                    </td>
                    <td>
                        <div class="form-group">
                            <input type="number" class="form-control" placeholder="Input Vacants" v-model="form.vacants">
                        </div>
                    </td>
                    <td>
                        <div class="form-group">
                            <button class="btn btn-success btn-sm" @click="submit"><i class="bi-plus"></i></button>
                        </div>
                    </td>
                </tr>
            </tfoot>
        </table>
    </div>
</template>
<script>
    export default {
        name: 'postinglist',
        data() {
            return {
                postings: [],
                form:{
                    job_name: null,
                    job_description: null,
                    vacants: 0
                }
            }
        },
        created(){
            this.postinglist()
        },
        mounted(){
            // this.postings1();
        },
        methods:{
            postinglist(){
                axios.get('http://127.0.0.1:8000/api/get_data').then(res => {
                    this.postings = res.data.data
                    // console.log(this.postings)
                })
            },
            submit(){
                const vm = this.postinglist;
                const frms = this.form;
                axios.post('http://127.0.0.1:8000/api/save_data',this.form)
                .then(function (response){
                    vm(),
                    // vm.push(response.data.data);
                    frms.job_name= null,
                    frms.job_description= null,
                    frms.vacants= 0
                })
                .catch(function (error){
                        console.log(error)
                });
            }
        }
    }

</script>