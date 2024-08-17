<template>
  <h1>Agenda de datos</h1>
  <br>
  <span>Filtro:</span>
  <input v-model="filtrotxt" type="text" @input="filtrar()"/>
  <br><br>
  <table class="bordered-table">
    <thead>
      <tr>
        <th>
          ID <br><br>
          <button @click="guardarUsuario()">Guardar Nuevo</button> <br><br>
          <button @click="guardarEditarUsuario()">Guardar Editar</button>
        </th>
        <th>
          NAME <br><br>
          <input v-model="usuarioObj.name" type="text" /><br><br>
          <input v-model="usuarioEditarObj.name" type="text" />
        </th>
        <th>
          EMAIL <br><br>
          <input v-model="usuarioObj.email" type="text" /><br><br>
          <input v-model="usuarioEditarObj.email" type="text" />
        </th>
        <th>
          ADDRESS <br><br>
          <input v-model="usuarioObj.address" type="text" /><br><br>
          <input v-model="usuarioEditarObj.address" type="text" />
        </th>
        <th>
          PHONE <br><br>
          <input v-model="usuarioObj.phone" type="text" /><br><br>
          <input v-model="usuarioEditarObj.phone" type="text" />
        </th>
        <th>
          COUNTRY <br><br>
          <input v-model="usuarioObj.country" type="text" /><br><br>
          <input v-model="usuarioEditarObj.country" type="text" />
        </th>
        <th>
          CITY <br><br>
          <input v-model="usuarioObj.city" type="text" /><br><br>
          <input v-model="usuarioEditarObj.city" type="text" />
        </th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(usuario, index) in filtrar()" :key="usuario.id">
        <td>{{ usuario.id }}</td>
        <td>{{ usuario.name }}</td>
        <td>{{ usuario.email }}</td>
        <td>{{ usuario.address }}</td>
        <td>{{ usuario.phone }}</td>
        <td>{{ usuario.country }}</td>
        <td>{{ usuario.city }}</td>
        <th>
          <button @click="editarUsuario(usuario, index)">editar</button>
          <button @click="eliminar(index)">eliminar</button>
        </th>
      </tr>
    </tbody>
  </table>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {

  },
  data() {
    return {
      filtrotxt: '',
      indexUsuario: '',
      listaFiltrada: [],
      usuarioObj: {
        id: '',
        name: '',
        email: '',
        address: '',
        phone: '',
        country: '',
        city: ''
      },
      usuarioEditarObj: {
        id: '',
        name: '',
        email: '',
        address: '',
        phone: '',
        country: '',
        city: ''
      },
      usuarios: [
        {
          id: 1,
          name: "Alice Johnson",
          email: "alice.johnson@example.com",
          address: "123 Maple Street",
          phone: "123-456-7890",
          country: "USA",
          city: "New York"
        },
        {
          id: 2,
          name: "Bob Smith",
          email: "bob.smith@example.com",
          address: "456 Oak Avenue",
          phone: "987-654-3210",
          country: "Canada",
          city: "Toronto"
        },
        {
          id: 3,
          name: "Carol White",
          email: "carol.white@example.com",

          address: "789 Pine Road",
          phone: "555-123-4567",
          country: "UK",
          city: "London"
        },
        {
          id: 4,
          name: "David Brown",
          email: "david.brown@example.com",
          address: "321 Elm Street",
          phone: "444-555-6666",
          country: "Australia",
          city: "Sydney"
        },
        {
          id: 5,
          name: "Emily Davis",
          email: "emily.davis@example.com",
          address: "654 Spruce Lane",
          phone: "333-444-5555",
          country: "USA",
          city: "Los Angeles"
        }
      ]
    }
  },
  methods: {
    filtrar() {
      return this.usuarios.filter(item => 
        item.name.toLowerCase().includes(this.filtrotxt.toLowerCase()) ||
        item.email.toLowerCase().includes(this.filtrotxt.toLowerCase())
      );
    },
    guardarUsuario() {
      this.usuarioObj.id = this.usuarios[this.usuarios.length - 1].id + 1;
      this.usuarios.push(this.usuarioObj);
      this.resetUserObj();
    },
    resetUserObj() {
      this.usuarioObj = {};
    },
    editarUsuario(usuario, index) {
      this.indexUsuario = index;
      this.usuarioEditarObj = {
        id: usuario.id,
        name: usuario.name,
        email: usuario.email,
        address: usuario.address,
        phone: usuario.phone,
        country: usuario.country,
        city: usuario.city
      }
    },
    guardarEditarUsuario() {
      this.usuarios[this.indexUsuario] = this.usuarioEditarObj;
      this.usuarioEditarObj = {};
    },
    eliminar(index) {
      this.usuarios.splice(index, 1);
    }
  }
}
</script>

<style scoped>
table {
  width: 100%;
}

.bordered-table {
  border: 1px solid gray;
  border-collapse: collapse;
}

.bordered-table th,
.bordered-table td {
  border: 1px solid gray;
  padding: 10px;
}

.bordered-table thead {
  background-color: #ddd;
}
</style>
