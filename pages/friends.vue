<template>
    <div class="body">
        <NavBar/>
        <ValoEditFriend :friend="selectedFriend"/>
        <ValoDeleteFriend :friend="selectedFriend" @onDeleted="getAll"/>
        <div class="container"><br>
            <a href="/dashboard" class="btn btn-secondary btn-sm"> Back to Dashboard</a><br><br>
            <h1 style="color: black;">
                My Friends
                <ValoAddFriend class="float-right" @onAdd="getAll"/>
            </h1>
            

            <table class="table table-boredered tabled-striped">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Tag ID</th>
                        <th>Username</th>
                        <th>Tag Name</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class="info" v-for="friend in friends" :key="friend.id">
                        <td>{{friend.tag_id}}</td>
                        <td>{{friend.user_name}}</td>
                        <td>{{friend.tag_name}}</td>
                        <td>
                            <b-button @click="onEdit(friend)" variant="info" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(friend)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
   data(){
       return{
           friends:[],
           selectedFriend: {}
       }
   },
   methods:{
        async getAll(){
            await this.$axios.get('/api/friends')
            .then((res)=>{
                if(res.status==200) {
                    this.friends = res.data
                    console.log(this.friends)
                }
            })
        },
        onEdit(selectedFriend) {
            this.selectedFriend = selectedFriend;
            this.$bvModal.show('valoEditFriend')
        },
        onDelete(selectedFriend) {
            this.selectedFriend = selectedFriend;
            this.$bvModal.show('valoDeleteFriend')
        }
   },
   created(){
       this.getAll()
   }
}
</script>
