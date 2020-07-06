<template>
  <div>
    <form @submit.prevent="agregar">
      <h3>Agregar nota</h3>
      <input type="text" class="form-control mb-2" 
        placeholder="Nombre de la nota" v-model="nota.nombre">
      <input type="text" class="form-control mb-2" 
        placeholder="Descripción de la nota" v-model="nota.descripcion">
      <button class="btn btn-primary" type="submit">Agregar</button>
    </form>
  </div>
</template>

<script>
export default {
    data(){
        return{
            notas: [],
            nota: {
                nombre: '', descripcion: ''
            }
        }
    },
    methods:{
        agregar(){

            if(this.nota.nombre.trim() === '' || this.nota.descripcion.trim() === ''){
                alert('Debes completar todos los campos antes de guardar');
                return;
            }
            console.log(this.nota.nombre, this.nota.descripcion);
            const params = {
                nombre: this.nota.nombre, 
                descripcion: this.nota.descripcion
            }

            this.nota.nombre = '';
            this.nota.descripcion = '';
            axios.post('/notas',params).then(res => {
              this.notas.push(res.data);
            })
        }
    }
}
</script>

<style>

</style>