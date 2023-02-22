<template>
  <div id="app">
    <img class="imgCronometro" src="./assets/cronometro.png" alt="cronometro">
    <a class="timer">{{numero}}</a>
    <div class="btns">
      <button class="btn" @click="vai">{{btn}}</button>
      <button class="btn" @click="limpar">LIMPAR</button>
    </div>
    <div class="list" v-show="historico.length > 0">
      <ul>
        <li v-for="item in historico" :key="item">VOCÊ FEZ UMA PAUSA EM: {{item}}</li>
      </ul>
      <button @click="historico = []">Limpar histórico</button>
    </div>
  </div>

</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      numero: 0,
      btn: 'VAI',
      timer: null,
      sec: 0,
      min: 0,
      hour: 0,
      historico: []
    }
  },
  methods:{
    vai(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
        this.btn = 'VAI';
        this.historico.push(this.numero);
      } else {
        this.timer = setInterval(() => {
          this.rodarTimer();
        }, 1000);
        this.btn = 'PAUSAR'
      }
    },
    limpar(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
      }
      this.sec = 0;
      this.min = 0;
      this.hour = 0;
      this.numero = 0;
      this.btn = 'VAI';
      this.historico = [];
    },
    rodarTimer(){
      this.sec ++;
      if(this.sec === 60){
        this.sec = 0;
        this.min++;
      }
      if(this.min === 60){
        this.min = 0;
        this.hour++;
      }
      const formatHour = (this.hour < 10 ? '0'+this.hour : this.hour);
      const formatMin = (this.min < 10 ? '0' + this.min : this.min);
      const formatSec = (this.sec < 10 ? '0' + this.sec : this.sec);
      const format = formatHour + ':' + formatMin + ',' + formatSec;

      return this.numero = format;
    }
  }
}
</script>

<style> @import './styles/app.css';</style>
