<template>
  <div>
    <form  method="post">
        <h2>{{mensaje}}</h2>
      <label for="name">NOMBRE </label>
      <input type="text" v-model="datos.nombres" /><br />
      <label for="name">EDAD </label
      ><input type="text" v-model="datos.edad" /><br />
      <label for="name">EMAIL </label
      ><input type="text" v-model="datos.email" /><br />
      <label for="name">COMENTARIO </label
      ><textarea
        name=""
        id=""
        cols="30"
        rows="10"
        v-model="datos.comentario"
      ></textarea
      ><br />
      <input type="button" value="GUARDAR" @click="guardar()" />
    </form>
  </div>
</template>

<script>
import { mapState } from "vuex";
const axios = require("axios");
export default {
  data() {
    return {
      datos: {
        nombres: "",
        edad: "",
        email: "",
        lenguajes: [],
        pais: "D",
        documento: "dni",
        comentario: "",
      },

      valid: true,

      mensaje: "",
      alert: null,
    };
  },
  computed: {
    ...mapState({ listaPaises: (state) => state.listaPaises }),
    ...mapState({ listaDocumento: (state) => state.listaDocumento }),
  },
  methods: {
    async guardar() {
      this.alert = null;
      this.mensaje = "";
  
        await axios
          .post(
            `https://61b75f4e64e4a10017d18ae0.mockapi.io/registrodesafio`,
            this.datos
          )
          .then((rpta) => {
            
            if (rpta.status == 201 || rpta.status == 200) {
              this.mensaje =  "Registro exitosamete"
            } else {
              this.mensaje = "Error al registro"
            }
          })
          .catch((error) => {
            this.mensaje =  error.response.status + ": " + error.message
          });
        this.alert = true;
      
      this.$store.dispatch("obtenerRegistro");
     this.datos= {
        nombres: "",
        edad: "",
        email: "",
        lenguajes: [],
        pais: "D",
        documento: "dni",
        comentario: "",
      }
    },
  },
};
</script>

<style lang="css" scoped>
*{box-sizing:border-box;}

form{
	width:600px;
	padding:16px;
	border-radius:10px;
	margin:auto;
	background-color:#ccc;
  text-align: left;
}

form label{
	width:72px;
	font-weight:bold;
	display:inline-block;
}

form input[type="text"],
form input[type="email"]{
	width:80%;
	padding:3px 10px;
	border:1px solid #f6f6f6;
	border-radius:3px;
	background-color:#f6f6f6;
	margin:8px 0;
	display:inline-block;
}

form input[type="submit"]{
	width:100%;
	padding:8px 16px;
	margin-top:32px;
	border:1px solid #000;
	border-radius:5px;
	display:block;
	color:#fff;
	background-color:#000;
} 

form input[type="submit"]:hover{
	cursor:pointer;
}

textarea{
	width:100%;
	height:100px;
	border:1px solid #f6f6f6;
	border-radius:3px;
	background-color:#f6f6f6;			
	margin:8px 0;
	/*resize: vertical | horizontal | none | both*/
	resize:none;
	display:block;
}
</style>