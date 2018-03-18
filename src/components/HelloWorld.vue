<template>
  <div class="hello">

    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
          {{Tittle_}}
          </h1>
          <h2 class="subtitle">
          All Happy And Organized
          </h2>
         </div>
      </div>
     </section>
 
    <br> </br>

    <form @submit.prevent="adicionar(tarefa,posicao,complete)">
      <input v-model="tarefa" >
      <input type="number" v-model="posicao" size="35px" >
      <input type="submit">
    </form> 


    <ul>
     <l1 v-if="listas.tittle!==null" v-for="listas in listas">
        <div>
          <button @click="deletar()"> Delete </button>
            {{listas.tittle}}
           <input type="checkbox" v-model="listas.completas">
        </div>
      </l1>
    </ul>  
  
    <br> </br>

    <button @click.prevent="completadas_(listas.completas)"> Complete </button>
     <ul>
        <l1 v-for="item in listas_completadas">
          <div>
          {{item.tittle2}}
          </div>
       </l1>
     </ul>

  

    <button @click.prevent="nao_completadas_(listas.completas)" v-model="nao_completadas_.tittle3"> Not Complete </button>
     <ul>
        <l1 v-if ="complete==false"v-for="itemm in listas_naocompletadas">
          <div>
          {{itemm.tittle3}}
          </div>
       </l1>
     </ul>

    <button @click.prevent="del_comp()">Delete Completed </button>

    
  </div>


</template>

<script>
import "bulma/css/bulma.css";
export default {
  name: "Task List",
  data() {
    return {
      Tittle_:"Task List",
      listas:[
      ],

      listas_completadas:[
        {
        tittle2:" ",
        completas2:true,
        },
      ],

      listas_naocompletadas:[
        {
        tittle3:" ",
        completas3:false,
        },
      ],

      posicao:0,
      posicao2:0,
      tarefa:"",
      complete: false

    }
  },


  methods:{

    adicionar(tarefa,posicao,complete){
    this.listas.splice(posicao,0,{
      tittle: tarefa,
      completas: complete
    })
    this.tarefa = ""
  },
  /*
    priorizar(tarefa,posicao2){
    var del = this.listas.indexOf(tarefa)
    this.listas.splice(posicao2,0,listas[del])
  },
*/
  
    completadas_(){
    for(var i=0; i<this.listas.length;i++){
      if(this.listas[i].completas===true){
      this.listas_completadas.splice(i,i,
        {
        tittle2:this.listas[i].tittle,
        completas2:this.listas[i].completas
            
        })
      }
    }
    
  },


    nao_completadas_(){  
    for(var i=0; i<this.listas.length;i++){
      if(this.listas[i].completas===false){
      this.listas_naocompletadas.splice(i,i,
      {
        tittle3:this.listas[i].tittle,
        completas3:this.listas[i].completas         
       })
      }
    }
  },


    del_comp(){ 
    for(var i=0; i<(this.listas.length);i++){
      if(this.listas[i].completas===true){
      this.listas[i].tittle=null,
      this.listas[i].completas=null,
      this.tarefa=null
     }
    }
    for(var i=0; i<(this.listas_completadas.length);i++){
      if(this.listas_completadas[i].completas2===true){
      this.listas_completadas[i].tittle2=""
     }
    }
  },

    deletar(tarefas){
    var del = this.listas.indexOf(tarefas)
    this.listas.splice(del,1)
  },


}

};



/*
  <form @submit.prevent="adicionar(posicao2,tarefa)">
  <input type="number" v-model="posicao2" >
  </form>
*/




</script>





<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: black;
}
  

</style>
