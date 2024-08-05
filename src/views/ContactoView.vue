<template>
    <div>
      <h1>{{  titulo  }}</h1>
      <div class="filtro">
          Filtro: <input type="search" v-model="textBuscar">
      </div>
      <table>
        <thead>
          <tr>
            <th>id</th>
            <th>name</th>
            <th>email</th>
            <th>address</th>
            <th>phone</th>
            <th>country</th>
            <th>city</th>
            <th></th>
          </tr>
          <tr> 
            <th><input type="number" v-model="contactoNuevoOBJ.id"></th>
            <th><input type="text" v-model="contactoNuevoOBJ.name"></th>
            <th><input type="text" v-model="contactoNuevoOBJ.email"></th>
            <th><input type="text" v-model="contactoNuevoOBJ.address"></th>
            <th><input type="text" v-model="contactoNuevoOBJ.phone"></th>
            <th><input type="text" v-model="contactoNuevoOBJ.country"></th>
            <th><input type="text" v-model="contactoNuevoOBJ.city"></th>
            <th><button @click="guardarNuevo">Agregar</button></th>
          </tr>
          <tr v-if="indexParaEditar" != null> 
            <th><input type="number" v-model="contactoEditarOBJ.id"></th>
            <th><input type="text" v-model="contactoEditarOBJ.name"></th>
            <th><input type="text" v-model="contactoEditarOBJ.email"></th>
            <th><input type="text" v-model="contactoEditarOBJ.address"></th>
            <th><input type="text" v-model="contactoEditarOBJ.phone"></th>
            <th><input type="text" v-model="contactoEditarOBJ.country"></th>
            <th><input type="text" v-model="contactoEditarOBJ.city"></th>
            <th><button @click="guardarEdicion">Guardar Cambio</button></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(contacto, index) in listaContactosComputada" :key="contacto.id">
            <td>{{ contacto.id }}</td>
            <td>{{ contacto.name }}</td>
            <td>{{ contacto.email }}</td>
            <td>{{ contacto.address }}</td>
            <td>{{ contacto.phone }}</td>
            <td>{{ contacto.country }}</td>
            <td>{{ contacto.city }}</td>
            <td>
              <button @click="eliminarContacto(index)">Eliminar</button>
              <button @click="EditarContacto(contacto, index)">Editar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MiComponente',
    data() {
      return {
        titulo: ' Contactos',
        textBuscar: '',
        contactoNuevoOBJ: {
          id: 0,
          name: "",
          email: "",
          address: "",
          phone: "",
          country: "",
          city: "",
        },
        contactoEditarOBJ: {
          id: 0,
          name: "",
          email: "",
          address: "",
          phone: "",
          country: "",
          city: "",
        },
        indexParaEditar : null,
        contactos: [
          {id:1, name: "Alice Johnson", email: "alice.johnson@example.com", address: "123 Maple Street", phone: "123-456-7890", country: "USA", city: "New York"},
          {id:2, name: "Bob Smith", email: "bob.smith@example.com", address: "456 Oak Avenue", phone: "987-654-3210", country: "Canada", city: "Toronto"},
          {id:3, name: "Carol White",email: "carol.white@example.com",address: "789 Pine Road",phone: "555-123-4567",country: "UK",city: "London"},
          {id:4, name: "David Brown",email: "david.brown@example.com",address: "321 Elm Street",phone: "444-555-6666",country: "Australia",city: "Sydney"},
          {id:5, name: "Emily Davis",email: "emily.davis@example.com",address: "654 Spruce Lane",phone: "333-444-5555",country: "USA",city: "Los Angeles"}       
        ],
        message: 'Hola Mundo'
      }
    },
    components:{
      //Registro de componentes
    },
    methods: {
      //métodos
      guardarNuevo(){
        this.contactos.push(Object.assign({}, this.contactoNuevoOBJ));
      },
      eliminarContacto(index){
        this.contactos.splice(index, 1);
      },
      guardarEdicion(){
        this.contactos[this.indexParaEditar] = Object.assign({}, this.contactoEditarOBJ);
        this.indexParaEditar = null;
      },
      EditarContacto(contacto, index){
        this.indexParaEditar = index;
        this.contactoNuevoOBJ = Object.assign({}, contacto);
      },
    },
    computed: {
      //propiedades computades
      listaContactosComputada(){
        return this.contactos.filter (item => item.name.toLowerCase().includes(this.textBuscar.toLowerCase())||item.email.toLowerCase().includes(this.textBuscar.toLowerCase())||item.address.toLowerCase().includes(this.textBuscar.toLowerCase())||item.phone.toLowerCase().includes(this.textBuscar.toLowerCase())||item.country.toLowerCase().includes(this.textBuscar.toLowerCase())||item.city.toLowerCase().includes(this.textBuscar.toLowerCase()));
      }
    },
    props: {
      //propiedades del componente
    },
    emits:[] // eventos personalizados
  }
  </script>
  
  <style scope>
  h1 {
    color: #42b983;
  }
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    border: 1px solid #ddd;
    padding: 8%;
  }
  th {
    background-color: #f2f2f2;
    text-align: left;
  }
  </style>