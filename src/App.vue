  <template>
  <div id="app" class="container">
    <h1>Components Dinâmicos</h1>

    <button @click="componentSelecionado = 'Home'">Home</button>
    <button @click="componentSelecionado = 'PostLista'" >Posts</button>
    <button @click="componentSelecionado = 'Sobre'">Sobre</button>
    <button @click="componentSelecionado = 'Assincrono'">Assincrono</button>
    <keep-alive :include="'Sobre'" :max="2">
      <component :is="componentSelecionado" v-bind="propsAtuais"></component>
    </keep-alive>
<!-- ==================================================================== -->
    <!-- <h1>Forma Padrão</h1>
    <PostLista :posts="posts" />

    <hr>
    <h1>Slots com escopo</h1> -->

    <!-- <PostLista :posts="posts"> -->
      <!-- DESESTRUTURAÇÃO -->
      <!-- <template slot-scope="{ meuPost }">
        <h2>{{ meuPost.titulo }}</h2>
        <p>{{ meuPost.conteudo }}</p>
        <small>{{ meuPost.autor }}</small>
      </template>
    </PostLista>
    
    <hr> -->

    <!-- NOVA SINTAXE SLOTS -->
    <!-- <PostLista :posts="posts" v-slot="{ meuPost }">
        <h2>{{ meuPost.titulo }}</h2>
        <p>{{ meuPost.conteudo }}</p>
        <small>{{ meuPost.autor }}</small>
    </PostLista> -->


  </div>
</template>

<script>
import PostLista from './components/PostLista.vue'
import Home from './components/Home.vue'
import Sobre from './components/Sobre.vue'
export default {
  components: {
    Assincrono: () => ({
      component: new Promise((reject) => {
        setTimeout(() => {
          // resolve(import('./components/Assincrono.vue'))
          reject('Carregamento falhou')
        }, 2000)
      }),
      loading: { template: '<p>Carregando...</p>' },
      error: { template: '<p>Erro ao carregar component!</p>' },
      delay: 200,
      timeout: 3000 // Infinity
      }),
    PostLista,
    Home,
    Sobre 
  },
  data() {
    return {
      componentSelecionado: 'Home',
      posts: [
        { id: 1, titulo: 'Components no Vue', conteudo: 'Components são uma das peças mais importantes no Vue', autor: 'Matheus Rodrigues' },
        { id: 2, titulo: 'Distribuindo conteúdo com slots', conteudo: 'Slots podem ser usados como repositórios de código HTML', autor: 'Matheus Rodrigues' }
      ]
    }
  },
  computed: {
    propsAtuais() {
      return this.componentSelecionado === 'PostLista' 
        ? { posts: this. posts } 
        : {}
    }
  }
}
</script>
<style scoped>
  .container {
    width: 960px;
    margin: auto;
  }

</style>