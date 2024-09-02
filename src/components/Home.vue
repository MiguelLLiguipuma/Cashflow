<template>
    <Layout>
         <template #header>
            <Header></Header>
         </template>
         <template #resume>
          <Resume
               :total-label= "'Ahorro Total'"
               :label ="label"
               :amount="amount"
               :total-amount="totalAmount"
          >
        <template #graphic>
          <Graphic :amounts="amounts" @select ="select"/>
            
         
        </template>
        <template #action>
            <Action @create="create"></Action>
        </template>
        
        </Resume>
        </template>
        <template #movements>
          <Movements
            :movements="movements"
            @remove = "remove"
          />
        </template>
 <div>{{ amounts }}</div>
    </Layout>
   
        

</template>

<script>
import Layout from "@/components/Layout.vue";
import Header from "@/components/Header.vue";
import Resume from "./Resume/Index.vue";
import Movements from "./Movements/Index.vue";
import Action from "./Action.vue";
import Graphic from "./Resume/Graphic.vue"

export default {
    components:{
        Layout,
        Header,
        Resume,
        Movements,
        Action,
        Graphic,
    },

    data(){
      return{
        amount: null,
        label:null,
        movements: [],
      };
    
    },
    computed: {
      amounts(){
       const lastDays = this.movements
        .filter(m  => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate()-30);

          return m.time > oldDate;
        
        })
        .map(m => m.amount);

     return lastDays.map((m,i) => {
          const lastMovements = lastDays.slice(0,i+1);

          return lastMovements.reduce((suma,movement)=> {
            return suma + movement

          },0);
        });
      },
      totalAmount (){
      return this.movements.reduce((suma,m) => {
        return suma + m.amount;
      }, 0)

    },
    },
    
    mounted(){
      const movements = JSON.parse(localStorage.getItem("movements"));
      if (Array.isArray(movements)) {
        this.movements = movements.map(m =>{
        return{...m,time: new Date(m.time) };
      });

        
      }
      
      
    },
    
    methods:{
      create(movement){
        this.movements.push(movement);
        this.save();
      },
      remove(id){
       const index = this.movements.findIndex(m => m.id === id);
       this.movements.splice(index,1);

      },save (){
        localStorage.setItem("movements", JSON.stringify( this.movements));
      },
      select (el){
        console.log(el);
        this.amount = el;

      }
  
}
  
};


</script>


<style>
/* Estilos generales */
body {
  margin: 0;
  font-family: 'Arial', sans-serif;
  background-color: #f5f5f5;
}

/* Contenedor principal */
.home-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

/* Barra de navegación */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: var(--brand-blue, #0689b0);
  color: #fff;
}

.navbar .logo {
  font-size: 1.5rem;
  font-weight: bold;
}

.navbar .nav-links {
  list-style: none;
  display: flex;
  gap: 1.5rem;
}

.navbar .nav-links a {
  text-decoration: none;
  color: #fff;
  font-weight: bold;
}

/* Sección del encabezado principal */
.hero-section {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 3rem 2rem;
  background-color: #fff;
  text-align: center;
}

.hero-section h1 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.hero-section p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  color: #555;
}

.cta-button {
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  background-color: var(--brand-green, #04b500);
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.cta-button:hover {
  background-color: #038a00;
}

/* Sección de características */
.features {
  display: flex;
  justify-content: space-around;
  padding: 2rem;
  background-color: #e9e9e9;
}

.feature {
  width: 30%;
  text-align: center;
}

.feature h2 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

.feature p {
  font-size: 1rem;
  color: #666;
}

/* Pie de página */
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #333;
  color: #fff;
}

.footer p {
  margin: 0;
}

.footer .social-links {
  list-style: none;
  display: flex;
  gap: 1rem;
}

.footer .social-links a {
  text-decoration: none;
  color: #fff;
  transition: color 0.3s ease;
}

.footer .social-links a:hover {
  color: var(--brand-green, #04b500);
}
</style>
