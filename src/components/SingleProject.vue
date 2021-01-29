<template>
    <div class="project">
        <div class="actions">
            <h3 @click="showDetails">{{project.title}}</h3>
            <div class="icons">
                <span class="material-icons">edit</span>
                <span class="material-icons">delete</span>
                <span class="material-icons">done</span>

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
            detailsView: false
        }
    },
    methods: {
        showDetails(){
            if (this.detailsView == false){
                this.detailsView = true
            } else{
                this.detailsView = false
            }
                
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
</style>