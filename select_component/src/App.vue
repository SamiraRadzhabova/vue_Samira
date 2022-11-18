<template>
<div class="sel">
  <select-app :infos="infos" @selectCity="citySelect" :selected="selected"></select-app>
  <p class="city">City: {{selected}}</p>
</div>

</template>

<script>
import SelectApp from './components/SelectApp.vue';

export default {
  name: "App",
  components: {
    SelectApp
  },
  data(){
    return{
      infos:[
        {
          name: 'Kiev',
          value:1
        },
         {
          name: 'Kriviy Rih',
          value:2
        },
         {
          name: 'Dnepr',
          value:3
        },
         {
          name: 'Lviv',
          value:4
        },
        {
          name: 'Kharkiv',
          value:5
        },
        {
          name: 'Ivano-Frankivsk',
          value:6
        },
      ],
      selected:'City'
    }
  },
  methods:{
    citySelect(info){
      this.selected=info.name;
    }
  }
};
</script>

<style>
.sel{
 background-color: #fff;
    box-shadow: 6px 6px 20px rgba(0,0,0,0.1);
    width: 500px;
    height: 450px;
    margin-top: 100px;
    margin-left: 500px;
}
.city{
  font-size: 20px;
  margin-left: 100px;
  margin-top: 300px;
}

</style>
