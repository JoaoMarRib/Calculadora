<template>
  <div class="p-3 rounded" style="max-width: 400px; margin: 50px auto; background: #246;">
    
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-azul">
      {{ ValorCalculadora || 0 }}
    </div>

    <div class="row no-gutters">
      <div class="col-3" v-for="n in TeclasCalculadora" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-azul rounded Sombra-class"
          :class="{'bg-vue-laranja': ['C','*','/','-','+','%','='].includes(n)}"
          @click="action(n)">
          
          {{n}}
        </div>
      </div>
    </div>
    
  </div>
</template>

<script>

export default {
  name: 'Calcu-ladora',
  props: {
    msg: String
  },

  data() {
    return{
      ValorCalculadora: "",
      TeclasCalculadora:['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      Operador: null,
      PValorCalculadora: '',
    }
  },

  methods: {
    action(n){

       if(!isNaN(n) || n === '.'){
        this.ValorCalculadora += n + '';
      }
      if(n === 'C'){
        this.ValorCalculadora = '';
      }

      if(n === '%'){
        this.ValorCalculadora = this.ValorCalculadora / 100 + '';
      }

      if(['/','*','-','+'].includes(n)){
        this.Operador = n;
        this.PValorCalculadora = this.ValorCalculadora;
        this.ValorCalculadora = '';
      }

      if(n === '='){
        this.ValorCalculadora = eval(
          this.PValorCalculadora + this.Operador + this.ValorCalculadora
        );
        this.PValorCalculadora = '';
        this.Operador = null;
      }

    }
  }
}
</script>

<style scoped>
    .bg-vue-azul {
    background: #7db1e9;
  }
  .Sombra-class:hover {
    cursor: pointer;
    background: #000000;
  }
  .bg-vue-laranja{
    background: #e97509;
  }
</style>
