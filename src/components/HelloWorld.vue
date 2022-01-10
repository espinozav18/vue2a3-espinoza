<template>
  <div>
    <h2>Datos del desafio 12</h2>

    <table>
      <thead>
        <tr>
          <th>id</th>
          <th>Nombre</th>
          <th>Edad</th>
          <th>Email</th>
          <th>Pais</th>
          <th>Documento</th>
          <th>comentario</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="prod in productos" :key="prod.id">
          <td>{{ prod.id }}</td>
          <td>{{ prod.nombres }}</td>
          <td>{{ prod.edad }}</td>
          <td>{{ prod.email }}</td>
          <td>{{ listaPaises.find((element) => element.id === prod.pais).pais }}</td>
          <td> {{ listaDocumento.find((element) => element.id === prod.documento).doc }}</td>
          <td>{{ prod.comentario }}</td>
        </tr>
      </tbody>
    </table>
   
  </div>
</template>

<script>
const axios = require("axios");
import { mapState } from "vuex";
export default {
  async setup() {
    let listaItems = [];
    await axios
      .get(`https://61b75f4e64e4a10017d18ae0.mockapi.io/registrodesafio`)
      .then((rpta) => {
        //console.error(rpta.data);
        listaItems = rpta;
      })
      .catch((error) => {
        console.log(error.response.status + ": " + error.message);
      });
    //console.info(listaItems);
    const productos = await listaItems.data;
    return {
      productos,
    };
  },
  computed: {
    ...mapState({ listaPaises: (state) => state.listaPaises }),
    ...mapState({ listaDocumento: (state) => state.listaDocumento }),
  },
};
</script>

<style lang="css" scoped>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>