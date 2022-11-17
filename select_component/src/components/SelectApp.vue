<template>
    <div class="select">
       <p class="title" @click="showInfos">{{selected}}</p>
    <div class="infos" v-if="infosVisible">
        <p
        v-for="info in infos" :key="info.value" @click="selectCity(info)">{{info.name}}</p>
    </div>
    </div>
</template>

<script>
export default {
    name: "SelectApp",
    props:{
        infos: {
            type: Array,
            default: []
            },
        selected: {
            type: String,
            default:''
        }
    },
    data(){
        return{
            infosVisible:false
        }
    },
    methods:{
        showInfos(){
            this.infosVisible=!this.infosVisible;
        },
        selectCity(info){
            this.$emit('selectCity',info);
            this.infosVisible=false;
        },
        hideCity(){
            this.infosVisible=false;
        },
       
    },
    mounted(){
            document.addEventListener('click',this.hideCity.bind(this),true);
        },
    beforeDestroy(){
            document.addEventListener('click',this.hideCity);
        }
}
</script>

<style>
.select{
position: relative;
width: 200px;
text-align: center;
margin-left: 140px;
padding-top: 20px;
}
.title{
     border: solid 1px #000000;
     border-radius: 5px;
       width: 100%;
}
.infos{
    border: solid 1px #000000;
    border-radius: 5px;
    position: absolute;
    width: 100%;
    margin-top: 7px;
}
.infos p:hover{
    background: #243afe;
}
.select p{
    margin:0;
    color:rgb(0, 0, 0);
    font-size: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
}
</style>