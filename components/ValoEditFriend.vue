<template>
    <div>
        
        <b-modal id="valoEditFriend" title="Edit Friend" ok-title="Save" @ok="onSubmit">
            <form action="#">

                <b-form-group
                    label="Tag ID"
                    label-for="tag_id">
                    
                    <b-form-input id="tag_id" v-model="friend.tag_id" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="User Name"
                    label-for="user_name">
                    
                    <b-form-input id="user_name" v-model="friend.user_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Tag Name"
                    label-for="tag_name">
        
                    <b-form-input id="tag_name" v-model="friend.tag_name" trim></b-form-input>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        friend: {}
    },


    methods: {
        async onSubmit(){
            await this.$axios.put('/api/friends/' + this.friend.id, this.friend)
            .then((res)=>{
                if(res.status==202) {
                    alert('Update Succesful')
                    console.log(this.friend)
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>