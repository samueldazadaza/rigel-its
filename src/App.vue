<template>
  <div id="app">
    <div class="table-responsive-sm container-lg" id="contenedor-tabla">
      <input
        class="m-2 input"
        type="text"
        placeholder="Search ID movil"
        class="search-input"
        v-model="searchValue"
      />
      {{ searchValue }}

      <table class="table table-bordered table-hover table-sm fs-6">
        <thead class="">
          <tr>
            <th>#</th>
            <td>BUS</td>
            <td>System</td>
            <td>Description</td>
            <td>Date</td>
            <td>Days</td>
            <td>Inmovilized</td>
          </tr>
        </thead>

        <tbody class="fs-6">
          <tr
            v-for="(p, index) in post"
            v-bind:style="p.system_name == 'IT-SIRCI' ? 'color:blue' : ''"
            v-bind:style="p.system_name == 'IT-ITS' ? 'color:red' : ''"
          >
            <th>{{ index + 1 }}</th>
            <td>{{ p.vehicle_code }}</td>
            <td>{{ p.system_name }}</td>
            <td>{{ p.issue_description }}</td>
            <td>{{ p.date_created }}</td>
            <td>{{ p.days_off }}</td>
            <td
              v-bind:style="
                p.is_inmovilized_vehicle == true
                  ? 'background-color: #FBB0A0'
                  : ''
              "
            >
              {{ p.is_inmovilized_vehicle }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},
  data() {
    return {
      post: [],
    };
  },
  methods: {
    getPosts() {
      fetch('https://api-rigel.herokuapp.com/')
        .then((response) => response.json())
        .then((data) => (this.post = data.data.data));
      //console.log(datos)
    },
  },
  mounted() {
    this.getPosts();
  },
  computed: {
    userList() {
      if (this.searchValue.trim().length >= 0) {
        return this.users.filter();
      }
      this.users;
    },
  },
};
</script>
