<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="proj in projects" key="proj.id" >
        <ProjectCard :project="proj" @delete="handleDelete" />
      </div>
    </div>
    <div>
      <button>Create a New Project</button>
      <router-link to="/bananas"><button>Go to Home</button></router-link>
    </div>
  </div>    
</template>

<script>
import ProjectCard from '../components/ProjectCard.vue'
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: { ProjectCard },
  data(){
    return{
      projects: [],

    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((res)=> res.json())
    .then((data)=> this.projects = data)
    .catch(err => console.log(err))
  },
  methods:{
    handleDelete(id){
      this.projects = this.projects.filter((proj)=> {
        return proj.id !== id
      })
    }
  }

}
</script>
