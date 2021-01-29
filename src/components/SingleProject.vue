<template>
    <div class="project" :class="{ complete: project.complete }">
        <div class="actions">
            <h3 @click="showDetails">{{project.title}}</h3>
            <div class="icons">
                <router-link :to="{ name: 'EditProject', params: { id: }}">
                    <span class="material-icons">edit</span>
                </router-link>
                <span class="material-icons" @click="deleteProject">delete</span>
                <span class="material-icons tick" @click="toggleComplete">done</span>

            </div>
        </div>
        <div class="details" v-if="detailsView">
            <p>{{project.details}}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['project'],
    data(){
        return{
            detailsView: false,
            uri: "http://localhost:3000/projects/" + this.project.id
        }
    },
    methods: {
        showDetails(){
            if (this.detailsView == false){
                this.detailsView = true
            } else{
                this.detailsView = false
            }       
        },
        deleteProject(){
            fetch(this.uri, { method: 'DELETE' })
                .then(() => this.$emit('delete', this.project.id))
                .catch(err => console.log(err.message))
        },
        toggleComplete(){
            fetch(this.uri, { 
                method: 'PATCH',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({ complete: !this.project.complete })
                }).then(() => {
                    this.$emit('complete', this.project.id)
                }).catch(err => console.log(err))
        }
    }
}
</script>

<style>
    .project{
        margin: 20px auto;
        background: white;
        padding: 10px 20px;
        border-radius: 4px;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
        border-left: 4px solid #e90074;
    }
    h3{
        cursor: pointer;
    }
    .actions{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .material-icons{
        font-size: 24px;
        margin-left: 10px;
        color: #bbb;
        cursor: pointer;
    }
    .material-icons:hover{
        color: #777;
    }
    .project.complete {
        border-left: 4px solid #00ce89;
    }
    .project.complete .tick {
        color: #00ce89;
    }
</style>