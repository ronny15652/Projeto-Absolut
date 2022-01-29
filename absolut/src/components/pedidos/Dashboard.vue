<template>
  <div class="Burger-table">
      <div>
        <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Mesa:</div>
        <div>Produto:</div>
        <div>Quantidade:</div>
        <div>Ações:</div>
        </div>
        <div id="burger-table-rows">
          <div class="burger-table-row">
            <div class="order-number">1</div>
            <div>João</div>
            <div>1</div>
            <div id="pro">Maminha<p>descricao</p></div>
            <div>
              <ul>
                <li>1</li>
              </ul>
            </div>
            <div>
              <select name="status" class="status">
                <option value="">Selecione</option>
              </select>
              <button class="delete-btn">Cancelar</button>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  data () {
    return {
      pedidos: null,
      pedidos_id: null,
      status: []
    }
  }
}
</script>

<style scoped>
  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #burger-table-heading,
  #burger-table-row,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;  
  }

  #burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 5px solid #333;
  }

   #burger-table-heading div,
   .burger-table-row div {
     width: 19%;
   }

   .burger-table-row {
     widows: 100%;
     padding: 12px;
     border: 1px solid #ccc;
   }

   #burger-table-heading .order-id,
   .burger-table-row .order-number {
     width: 5%;
   }

   select {
     padding: 12px 6px;
     margin-right: 12px;
   }

   .delete-btn {
     background-color: #222;
     color: #FCBA03;
     font-weight: bold;
     border: 2px solid #222;
     padding: 10px;
     font-size: 16px;
     margin: 0 auto;
     cursor: pointer;
     transition: .5s;
   }
  
   .delete-btn:hover {
     background-color: transparent;
     color:#222;  
   }
</style>
