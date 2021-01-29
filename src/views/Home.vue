<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project=project @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from '../components/SingleProject.vue'

export default {
  name: 'Home',
  components: { SingleProject },
  data(){
    return{
      projects: []
    }
  },
  mounted(){
    fetch("http://localhost:3000/projects")
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id){
      this.projects = this.projects.filter((project) => {
        // if the deleted id and the id in the list dosent match the object is returned and if it is deleted the object is deleted
        return project.id !== id
      });
    },
    handleComplete(id){
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  }
}
</script>
