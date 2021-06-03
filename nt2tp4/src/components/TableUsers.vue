<template>

  <section class="src-components-table-users">
    <div class="jumbotron">
      <table class="table">
        <thead>
          <th>Nombre</th>
          <th v-if="this.hasAge">Edad</th>
          <th v-if="this.hasPhone">Telefono</th>
          <th>Mail</th>
        </thead>
        <tbody>
          <tr v-for="(user, index) in usersToShow" :key="index">
            <td>{{user.name}}</td>
            <td v-if="hasAge">{{user.age}}</td>
            <td v-if="hasPhone">{{user.phone}}</td>
            <td>{{user.email}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-table-users',
    props: ['usersToShow', 'options'],
    mounted () {

    },
    data () {
      return {
        hasAge: this.options.hasAge,
        hasPhone: this.options.hasPhone
      }
    },
    methods: {
      
    },
    computed: {

    }
}


</script>


