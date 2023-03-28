<template>
    <div class="project">
        <div class="actions">
            <h3 @click="showDetails = !showDetails">- {{ project.title }} -</h3>
            <div class="icons">
                <span @click="" class="material-icons">edit</span>
                <span @click="deleteProject" class="material-icons">delete</span>
                <span @click="" class="material-icons">done</span>
            </div>
        </div>
        <div v-if="showDetails" class="details">
            <p>{{ project.details }}</p>
        </div>

    </div>
</template>

<script>

    export default {
        props:['project'],
        data(){
            return {
                showDetails: false,  
                uri: 'http://localhost:3000/projects/'+ this.project.id  ,            
            }
        },
        methods:{
            deleteProject(){
                fetch(this.uri, { method: 'DELETE' })
                .then(()=> this.$emit('delete', this.project.id))
                .catch((err)=> console.log(err))
            },
        }
        
        
    }
</script>

<style>
    h3 {
        cursor: pointer;
        color: rgb(4, 4, 81);
    }
    .project {
        
        margin: 20px auto;
        background: white;
        padding:10px 20px;
        border-radius: 4px;
        box-shadow: 1px 2px 3px rgba(0,0,0,0.5);
        border-left: 4px solid #e90074;
    }
    .material-icons{
        font-size: 24px;
        cursor: pointer;
        margin-left: 5px;
    }
    .material-icons:hover{
        font-size: 36px;
        color: #e90074;

    }
    .actions{
        display: flex;
        justify-content: space-between;
        align-items: center ;
    }
    /* .details {
        display: none;
    }

    .project:hover .details {
        display: block;
    } */

</style>