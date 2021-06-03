<template>

  <section class="src-components-random-users">

    <div class="jumbotron">
      <button @click="fetchByXML()" type="button" class="btn btn-primary">Fetch by XMLHttpRequest</button>
      <button @click="fetchByAxios()" type="button" class="btn btn-primary">Fetch by axios</button>
      <button @click="fetchByFetch()" type="button" class="btn btn-primary">Fetch by direct fetch</button>
      <button @click="refreshData()" type="button" class="btn btn-warning"> Limpiar información </button>
      <br/><br/>
      <p class="alert alert-danger" v-if="this.errors"> {{ this.errors}} </p>
      <TableUsers v-bind:usersToShow="this.usersToShow" v-bind:options="{hasAge: false, hasPhone: true}" />
      

    </div>

  </section>

</template>

<script lang="js">

  import TableUsers from './TableUsers';


  export default  {
    name: 'src-components-random-users',
    components: {
      TableUsers
    },
    props: [],
    mounted () {

    },
    data () {
      return {
        urlToFetch: 'https://60b54a9dfe923b0017c83dfb.mockapi.io/api/users/user',
        usersToShow: {},
        errors: undefined
      }
    },
    methods: {
      refreshData() {
        this.usersToShow = {};
        this.errors = undefined;
      },

      fetchByXML() {

        let request = new XMLHttpRequest();
        request.open('get',this.urlToFetch);

        request.addEventListener('load',() =>{
          if(request.status == 200){
            this.usersToShow = JSON.parse(request.response);
          }
          else{
            this.error = request.responseText;
          }
        });

        request.send()
      },

      fetchByAxios() {
        this.axios(this.urlToFetch)
        .then(rsp => {
          this.usersToShow = rsp.data;
        })
        .catch(err => {
          this.errors = err;
        });
      },

      fetchByFetch() {
        
        fetch(this.urlToFetch)
          .then(response => {
            response.json().then(rsp => {
              this.usersToShow = rsp;
            })
            .catch(err => {
              this.errors = err;
            });
          })
          .catch(error => console.error(error));
      }

    },
    computed: {
      
    }
}


</script>

<style scoped lang="css">

</style>
