<template>
   <div class="container">
    <Message :msg="msg" v-show="msg"/>
    <div class="content">
        <form  id="burguer-form" method="POST" @submit="createBurguer">
            <div class="input-container">
                <label for="name">Client name:</label>
                <input type="text" id="name" name="name" v-model="name" placeholder="Write your name">
              
            </div>
            <div class="input-container">
                <label for="bread">Chose your bread:</label>
                <select name="bread" id="bread" v-model="bread">
                    <option value="">Select your bread</option>
                    <option v-for="bread in breads" v-bind:key="bread.id" :value="bread.class">{{ bread.type }}</option>
                </select>
                <div :class="bread"></div>
            </div>

            <div class="input-container">
                <label for="meat">Chose your Burguer´s meat:</label>
                <select name="meat" id="meat" v-model="meat">
                    <option value="">Select kind of meat</option>
                    <option v-for="meat in meats" v-bind:key="meat.id" :value="meat.class">{{meat.type}}</option>
                </select>
                <div :class="meat"></div>
            </div>

            <div class="input-container" id="opcionais-container">
                <label id="opcionais-title" for="optional">Select your options:</label>
                <div class="checkbox-container" v-for="option in optionaldata" :key="option.id">
                    <input type="checkbox" name="optional" v-model="optional" :value="option.type">
                    <span>{{ option.type }}</span>
                <div class="img-option" >
                    <img :src="option.img" :alt="option.classe">
                </div>
                </div>
                
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Create my Burguer!" >
            </div>
        </form>
        
    </div>
   </div>
</template>
<script>
import Message from './Message.vue';

export default {
    name:"BurguerForm",
    data(){
        return{
            breads:null,
            meats:null,
            optionaldata:null,
            name:null,
            bread:null,
            meat:null,
            optional:[],
            status:"Solicited",
            msg:null,
            selectecOption:[]
          
        }
    },

    methods:{
      
        async getIngredient(){
            const req = await fetch("http://localhost:3000/ingredients");
            const data = await req.json()
            this.breads = data.breads
            this.meats = data.meats
            this.optionaldata = data.optional
      

        },
        async createBurguer(e){
          e.preventDefault()
          
          const data = {
            name: this.name,
            meat: this.meat,
            bread: this.bread,
            optional: Array.from(this.optional),
            status:"Solicited",
          }
          const dataJson = JSON.stringify(data)
          console.log(this.optional);

          const req = await fetch("http://localhost:3000/burgers", {
            method: "POST",
            headers: {"content-Type": "application/json"},
            body: dataJson
          });

          const res = await req.json()
          
          //put a system message
          this.msg = `Order Nº ${res.id}  realized sucessfully!`
          //clear message
          setTimeout(()=> this.msg="", 3000)
          //clean inputs
          this.name = "";
          this.bread = "";
          this.meat = "";
          this.optional = [];
          
          
        },
        getImagePath(options){
  
          console.log(options);
      
          return  `/../../public/img/${options}.png`
        }
    },
    mounted(){
        this.getIngredient()
    },
    components:{
      Message
    }
    
}
</script>
<style scoped>

.img-option img{
  border-bottom: 1px solid rgba(0, 0, 0, 0.336);
  border-radius: 10px;
  width: 70px;
  min-height: 30px;
  margin-left: 10px;
}
.img-option img{
  width: 30px;
  height: 30px;
}
.italiano-branco{
  background-image: url("../../public/img/paoitaliano.png");
    background-size: cover;
    background-position: center;
    height: 60px;
    width: 70px;
    margin-top: 20px;
    border: 2px solid rgba(0, 0, 0, 0.336);
    border-radius: 10px;
}
.parmesao-oregano{
  background-image: url("../../public/img/paogergelim.png");
    background-size: cover;
    background-position: center;
    height: 50px;
    width: 70px;
    margin-top: 20px;
    border: 2px solid rgba(0, 0, 0, 0.336);
    border-radius: 10px;
}

.picanha{
  background-image: url("../../public/img/picanha.png");
    background-size: cover;
    background-position: center;
    height: 60px;
    width: 80px;
    margin-top: 20px;
    border: 2px solid rgba(0, 0, 0, 0.336);
    border-radius: 10px;
}
.alcatra{
  background-image: url("../../public/img/alcatra.jpg");
    background-size: cover;
    background-position: center;
    height: 40px;
    width: 100px;
    margin-top: 20px;
    border: 2px solid rgba(0, 0, 0, 0.336);
    border-radius: 10px;
}
.maminha{
  background-image: url("../../public/img/maminha.jpg");
    background-size: cover;
    background-position: center;
    height: 60px;
    width: 80px;
    margin-top: 20px;
    border: 2px solid rgba(0, 0, 0, 0.336);
    border-radius: 10px;
}
.veggie-burger{
  background-image: url("../../public/img/veggie.png");
    background-size: cover;
    background-position: center;
    height: 60px;
    width: 80px;
    margin-top: 20px;
    border: 2px solid rgba(0, 0, 0, 0.336);
    border-radius: 10px;
}
.container{
    display: flex;
    justify-content: center;
    align-items: center;
  flex-direction: column;
}
.content{
  display: flex;
  justify-content: center;
 align-items: center;
 flex-direction: row;
}
 #burger-form {
    max-width: 600px;
 

  }

  .input-container {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }

  input, select {
    padding: 5px 10px;
    width: 600px;
  }

  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #opcionais-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-content: flex-start;
    align-items: center;
    justify-content: center;
    width: 30%;
    margin-bottom: 20px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 1px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>