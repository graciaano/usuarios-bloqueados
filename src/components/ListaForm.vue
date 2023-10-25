<template>
  <div id="app">
    <div class="content-container">
    <div class="page-tittle">Usuários Bloqueados</div>
    <div class="custom-table-container">
      <div class="custom-table">
        <table class="table-space" cellspacing="0" >
          <thead>
            <tr>
              <th>
                <input type="checkbox" v-model="marcarTodos" @change="marcarTodosCheckbox" />
              </th>
              <th class="color-name" @click="ordenarPor('nome')" :class="{ 'asc': colunaOrdenada === 'nome' && ordemAscendente, 'desc': colunaOrdenada === 'nome' && !ordemAscendente }">Nome</th>
              <th class="color-name" @click="ordenarPor('empresa')" :class="{ 'asc': colunaOrdenada === 'empresa' && ordemAscendente, 'desc': colunaOrdenada === 'empresa' && !ordemAscendente }">Empresa</th>
              <th class="color-name" @click="ordenarPor('numero')" :class="{ 'asc': colunaOrdenada === 'numero' && ordemAscendente, 'desc': colunaOrdenada === 'numero' && !ordemAscendente }">Numero</th>
              <th class="color-name">Excluir <button v-show="marcarTodos" @click="excluirItensSelecionados" class="delete-button-selecionado">
                  <i class="fas fa-trash-alt" style="color: red;"></i> Excluir
                </button>
              </th> 
            </tr>
          </thead>
          <tbody>
            <tr class="aling-name" v-for="(item, index) in items" :key="index">
              <td class="checkbox-cell">
                <input type="checkbox" v-model="item.selecionado"  />
              </td>
              <td>
                {{ item.nome }}
              </td>
              <td>
                {{ item.empresa }}
              </td>
              <td>
                {{ item.numero }}
              </td>
              <td class="delete-button-container">
                <button @click="excluirItem(index)" class="delete-button">
                  <span class="delete-icon"> X </span>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
        </div>
      </div>
    </div>
  </div>
</template>

  <script>
  export default {
    data() {
      return {
        items: [],
        colunaOrdenada: '',
        ordemAscendente: true,
        marcarTodos: false
      };
    },

    created (){
        this.items = [
          {nome: 'aaaaaaaaaa', empresa: 'ndyassylcsiii', numero: '5432426824564', selecionado:false },
          {nome: 'aaaaaaaaaa', empresa: 'ndyassylcsiii', numero: '5432426824564', selecionado:false },
          {nome: 'aaaaaaaaaa', empresa: 'ndyassylcsiii', numero: '5432426824564', selecionado:false },
          {nome: 'aaaaaaaaaa', empresa: 'ndyassylcsiii', numero: '5432426824564', selecionado:false },
          {nome: 'aaaaaaaaaa', empresa: 'ndyassylcsiii', numero: '5432426824564', selecionado:false },
          {nome: 'aaaaaaaaaa', empresa: 'ndyassylcsiii', numero: '5432426824564', selecionado:false },

  
        ];
    },

      methods: {
    excluirItem(index) {
      if (this.items[index].selecionado) {
        this.items.splice(index, 1);
      }
    },
    excluirItensSelecionados() {
      this.items = this.items.filter(item => !item.selecionado);
    },
      ordenarPor(coluna) {
        if (this.colunaOrdenada === coluna) {
          this.ordemAscendente = !this.ordemAscendente;
        } else {
          this.ordemAscendente = true;
        }
  
        this.colunaOrdenada = coluna;
  
        this.items.sort((a, b) => {
          const valorA = a[coluna].toLowerCase();
          const valorB = b[coluna].toLowerCase();
          if (valorA < valorB) {
            return this.ordemAscendente ? -1 : 1;
          }
          if (valorA > valorB) {
            return this.ordemAscendente ? 1 : -1;
          }
          return 0;
        });
      },
      marcarTodosCheckbox() {
        this.items.forEach(item => (item.selecionado = this.marcarTodos));

      }
    }
  }
  </script>
  
  <style scoped>

  th{
  padding: 5px 5px 5px 5px;
  }

  .asc::after {
      content: '↑';
    }
  
    .desc::after {
      content: '↓';
    }
  
    .delete-button {
      background-color: transparent;
      color: transparent;
      border: none;
      padding: 1px ;
      cursor: pointer;
    }

    .delete-icon {
      color: red;
    }
  
    .delete-button:hover {
      background-color: transparent;
    }
    .custom-table-container {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 40vh;
      background-color: white;
      background-attachment: fixed;
    }

    .custom-table {
      font-family: Arial, Helvetica, sans-serif;
      border-radius: 10px ;
      background-color: #fff;
      padding: 1px;
      height: 75vh;
      box-shadow: 1px 1px 2px 2px #d9d9d9;


    }

    td {
      border: 0.5px solid #554f4f;
      border-collapse: 0.5px solid #554f4f;
      padding: 2px 75px;
      height: 20px;
    }

    .page-tittle {
      font-size: 2rem;
      font-weight: 700;
      display: flex;
      justify-content: center;
      padding: 0;
      height: 70px;
      align-items: center;
      align-content: center;

    }

    .page-tittle {
      width: 54vw;
    }

    .content-container {

      position: relative;

    }

    .color-name {
      color: #2bb542;
      text-align: left;
    }

    .checkbox-cell {
      padding: 5px;
    }


    .aling-name {
      text-align: left;
    }

    .table-space {
      padding: 0px;
    }

  



  </style>
