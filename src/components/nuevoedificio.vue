<template>
    <div id="div-nuevo-edificio">
        <h2>Agregar Edificio</h2><br>
        <form v-on:submit.prevent="guardar">
            <label>Nombre del edificio:</label>
            <input type="text" v-model="edificio.nombre"><br>
            <label>Altura del edificio:</label>
            <input type="text" v-model.number="edificio.altura"><br>
            <label>Año de construcción:</label>
            <input type="text" v-model.number="edificio.ano"><br>
            <label>País:</label>
            <input type="text" v-model="edificio.pais"><br>
            <label>Descripción:</label>
            <input type="text" v-model="edificio.descripcion"><br>
            <label>Imagen:</label>
            <input type="text" v-model="edificio.srcimagen"><br>
            <label>Texto alternativo Imagen:</label>
            <input type="text" v-model="edificio.altimagen"><br>            
            <div id="div-boton">
                <button type="submit">Guardar</button>
            </div>
            <div id="div-saludo" v-on:click="saludar">Enviar Saludo</div>                                                
        </form>
    </div>
</template>


<script>
import axios from 'axios'
export default {
    name: 'nuevoedificio',
    data: function() {
        return {
            edificio: {
                nombre: "",
                altura: "",
                ano: "",
                pais: "",
                descripcion: "",
                srcimagen: "",
                altimagen: ""
            }
        }
    },
    methods: {
        guardar: function() {
            this.$emit('anexar', this.edificio)
        },
        saludar: function() {
            axios.get("http://localhost:8000/saludo")
            .then(respuesta => {
                let texto = respuesta.data.mensaje
                alert(texto);
            })
        }
    }
    
}
</script>


<style scoped>
#div-nuevo-edificio {
    margin-top: 50px;
    width: 40%;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
}

input {
    margin-bottom: 10px;
}

label {
    display: inline-block;
    width: 250px;
    text-align: left;
}

#div-boton {
    text-align: right;
}

#div-saludo {
    border: 1px solid #000000;
    cursor:pointer;
}
</style>