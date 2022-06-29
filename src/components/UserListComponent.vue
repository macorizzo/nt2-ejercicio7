<template>

  <section class="jumbotron jumbotron-fluid">
    <h1>Lista de usuarios</h1>


    <div v-if="!users.length">
      <div class="alert alert-danger">
        No hay usuarios disponibles
      </div>
    </div>


    <table v-else class="table table-striped">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Nombre</th>
          <th scope="col">Email</th>
          <th scope="col">Telefono</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, i) in users" :key="i">
          <th scope="row">{{ user.id }}</th>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.phoneNumber }}</td>
        </tr>
      </tbody>
    </table>


  </section>

</template>

<script lang="js">

export default {
  name: 'user-list-component',
  props: [],
  beforeMount() {
    this.getUsersAxios();

  },
  data() {
    return {
      url: 'https://629d30e03798759975e10eeb.mockapi.io/api/v1/postusers',
      users: [],
    }
  },
  methods: {
    async getUsersAxios() {
      try {
        this.users = [];
        const { data } = await this.axios(this.url);
        this.users = data;
      } catch (e) {
        console.error(e, 'axios');
      }
    },
  },
  computed: {

  }
}


</script>

<style scoped lang="css">
.jumbotron {
  background-color: lightgrey;
}

.bg-color {
  width: 100vw;
  height: 100vh;
  background-color: pink;
}

.table-striped tbody tr:nth-of-type(odd) {
  background-color: rgb(165, 75, 75);
}

.table-striped tbody tr:nth-of-type(even) {
  background-color: rgb(63, 65, 63);
}
</style>