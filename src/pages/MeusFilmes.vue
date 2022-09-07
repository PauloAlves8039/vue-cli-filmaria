<template>
  <div id="meus-filmes">
    <h1>Meus Filmes</h1>
    <span v-if="filmes.length"> Você não possui nenhum filme salvo! </span>
    <ul>
      <li v-for="filme in filmes" :key="filme.id">
        <span>{{filme.nome}}</span>
        <div>
          <router-link tag="button" :to="`/filme/${filme.id}`">Ver detalhes</router-link>
          <button @click="excluir(filme.id)">Excluir</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filmes: [],
    };
  },
  created(){
    const minhaLista = localStorage.getItem('myFilme');
    this.filmes = JSON.parse(minhaLista) || [];
  },
  methods:{
    excluir(id){
      let filtroFilmes = this.filmes.filter((filme) => {
        return (filme.id !== id);
      });
      return this.filmes = filtroFilmes;
    }
  },
  watch:{
    filmes(){
      localStorage.setItem('myFilme', JSON.stringify(this.filmes));
    }
  }
};
</script>

<style scoped>

#meus-filmes {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
}

ul {
  padding: 0;
}

ul li {
  padding: 0;
  list-style: none;
  min-width: 600px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

span {
  font-size: 25px;
}

button {
  margin-right: 5px;
  border-radius: 5px;
  margin-top: 15px;
  cursor: pointer;
  border: 0;
  padding: 12px;
  font-size: 18px;
  transition: all 0.5s;
  outline: none;
}

button:hover {
  background: brown;
  color: #fff;
}

</style>