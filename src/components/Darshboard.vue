<template>
    <div>
      <Message class="delete" :msg="msg" v-show="msg"/>
        <div id="burgur-table">
            <div>
                <div id="burger-table-heading">
                    <div class="order-id">#:</div>
                    <div>Client</div>
                    <div>Bread</div>
                    <div>Meat</div>
                    <div>Optionals</div>
                    <div>Actions</div>
                </div>
            </div>
            <div id="burger-table-rows">
                <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
                    <div class="order-number">{{burger.id}}</div>
                    <div>{{ burger.name }}</div>
                    <div>{{ burger.bread }}</div>
                    <div>{{ burger.meat }}</div>
                    <div>
                        <ul>
                            <li v-for="(option, index) in burger.optional" :key="index">{{ option }}</li>
                           
                        </ul>
                    </div>
                    <div>
                        <select name="status" class="status" @change="updatedBurger($event, burger.id)">
                            <option  v-for="statusBurguer in status" :key="statusBurguer.id" :value="statusBurguer.type" :selected="burger.status == statusBurguer.type">{{statusBurguer.type}}</option>
                        </select>
                        <button class="delete-btn" @click="deleteBurguer(burger.id)">Delete</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';

export default {
    name:"Darshboard",
    components:{Message},
    data(){
      return{
        burgers:null,
        burger_id:null,
        status: [],
        msg:""
      }
    },
    methods:{
      async getOrders(){
        const req = await fetch("http://localhost:3000/burgers");

        const data = await req.json();

        this.burgers = data
        
        

        //get status
        
       
        
        
      },
      async getStatus(){

        const reqStatus = await fetch("http://localhost:3000/status");
        const dataStatus = await reqStatus.json();
        this.status = dataStatus
},
async deleteBurguer(id){
  
  const req = await fetch(`http://localhost:3000/burgers/${id}`,{
    method:"DELETE"
  });

  const res = await req.json()

  //msg
  this.msg = `Order Nº ${id} deleted sucessfully`
  setTimeout(()=> this.msg = "", 3000)

  this.getOrders()
  
},
  async updatedBurger(e, id) {
    const option = e.target.value;

     const dataJson = JSON.stringify({status:option});
     const req = await fetch(`http://localhost:3000/burgers/${id}`,{
      method:"PATCH",
      Headers: {"Content-type" : "application/json"},
      body:dataJson
     });
     
     const res = req.json()

     console.log(res);
     
  }
    },
    mounted(){
      this.getOrders() 
      this.getStatus()
    }
}
</script>

<style scoped>
.delete{
  background-color: rgb(231, 81, 81);
  border: 2px solid rgb(231, 81, 81);
}

#burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #burger-table-heading,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #burger-table-heading div,
  .burger-table-row div {
    width: 19%;
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
    color:#fcba03;
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
    color: #222;
  }
</style>