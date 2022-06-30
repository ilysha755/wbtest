<template>
<v-app>
  <v-navigation-drawer app>
  </v-navigation-drawer>
  <v-main>
    <v-container fluid>
      <h3>Доставки</h3>
      <p>Как только выкуп оплачен, он моментально появится в доставках. Дальше мы отслеживаем его статус. "Доставлен" - можно забирать с пункта выдачи.</p>
      <v-tabs>
        <v-tab @click="typeDelivery = 'completed'; addItems()">Готовы к выдаче <v-badge></v-badge> </v-tab>
        <v-tab @click="typeDelivery = 'actived'; addItems()">В пути <v-badge></v-badge> </v-tab>
        <v-tab @click="typeDelivery = 'picked'; addItems()">Полученые <v-badge></v-badge> </v-tab>
        <v-tab @click="typeDelivery = 'rejected'; addItems()">Отменённые <v-badge></v-badge> </v-tab>
      </v-tabs>
 <v-container class="d-flex justify-center flex-wrap " fluid>
    <v-card max-width="368px" class=" ma-10 d-flex justify-sm-space-between flex-column" v-for="card in items" :key="card.id">

 <v-row class="d-flex justify-sm-space-between align-center">
  <v-col>
  <v-card-title class="grey--text">Заказ:</v-card-title>
  <v-card-subtitle class="">{{card.id}}</v-card-subtitle>
  </v-col>
  <v-col>
        <svg width="20" height="24" viewBox="0 0 20 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M17.3648 23.2791C18.3802 23.2791 19.2109 22.4487 19.2109 21.4329V9.00552C19.2109 7.99013 18.3802 7.15936 17.3648 7.15936H13.9032C13.534 7.15936 13.2109 7.48244 13.2109 7.85167V9.23629C13.2109 9.60552 13.534 9.92859 13.9032 9.92859H15.7494C16.1191 9.92859 16.4417 10.2517 16.4417 10.6214V19.8171C16.4417 20.1858 16.1191 20.5094 15.7494 20.5094H4.21462C3.84539 20.5094 3.52231 20.1858 3.52231 19.8171V10.6214C3.52231 10.2517 3.84539 9.92859 4.21462 9.92859H6.06077C6.43001 9.92859 6.75308 9.60598 6.75308 9.23629V7.85167C6.75308 7.48244 6.43001 7.15936 6.06077 7.15936H2.59924C1.58385 7.15936 0.753082 7.99013 0.753082 9.00552V21.4324C0.753082 22.4469 1.58385 23.2786 2.59924 23.2786H17.3648V23.2791Z" fill="#D3D3D3"/>
<path d="M11.3625 14.2606V5.30169H14.0851C14.5466 5.30169 14.7774 4.8863 14.5 4.65553L10.3462 0.824763C10.162 0.686301 9.88461 0.686301 9.70046 0.824763L5.54661 4.65553C5.26923 4.93246 5.5 5.30169 5.96153 5.30169H8.5923V14.2611C8.5923 14.6312 8.91538 15.0005 9.28461 15.0005H10.6692C11.0394 15 11.3625 14.6308 11.3625 14.2606Z" fill="#D3D3D3"/>
</svg>
  </v-col>

 </v-row>
<v-row class="d-flex justify-center align-center ma-5">
 
 <v-img max-width="64px" max-height="64px" :src="card.product.image" />
 
  <v-col>
<v-card-title class="">{{card.product.name}}</v-card-title>
      <v-card-subtitle class="light-blue--text">Арт. {{card.product.cod1S}}</v-card-subtitle>
  </v-col>
</v-row>
    <v-row class="ml-7">
      <v-chip :color="card.statusColor" width="176px" class="" label>{{card.statusLocalized}}</v-chip>
    </v-row>
     <v-row class="d-flex justify-center ma-5">
      <v-col class="">
<svg width="18" height="20" viewBox="0 0 18 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<path fill-rule="evenodd" clip-rule="evenodd" d="M13.4109 0.768617L13.4119 1.51824C16.1665 1.73413 17.9862 3.61119 17.9891 6.48975L18 14.9155C18.0039 18.054 16.0322 19.985 12.8718 19.99L5.15188 20C2.01119 20.004 0.0148166 18.027 0.0108673 14.8795L6.64975e-06 6.55272C-0.00394266 3.65517 1.75153 1.78311 4.50617 1.53024L4.50518 0.780611C4.5042 0.340832 4.83001 0.00999726 5.26444 0.00999726C5.69886 0.00899776 6.02468 0.338833 6.02567 0.778612L6.02666 1.47826L11.8914 1.47027L11.8904 0.770616C11.8894 0.330837 12.2152 0.00100177 12.6497 2.26549e-06C13.0742 -0.000997234 13.4099 0.328838 13.4109 0.768617ZM1.52149 6.86183L16.4696 6.84184V6.49202C16.4272 4.3431 15.349 3.21566 13.4139 3.04774L13.4148 3.81736C13.4148 4.24714 13.0801 4.58797 12.6556 4.58797C12.2212 4.58897 11.8944 4.24914 11.8944 3.81936L11.8934 3.00976L6.02865 3.01776L6.02963 3.82635C6.02963 4.25714 5.7048 4.59697 5.27038 4.59697C4.83595 4.59797 4.50915 4.25914 4.50915 3.82835L4.50816 3.05874C2.58287 3.25164 1.51755 4.38308 1.52051 6.55099L1.52149 6.86183ZM12.24 11.405V11.416C12.2499 11.8758 12.625 12.2246 13.0802 12.2146C13.5245 12.2036 13.879 11.8228 13.8691 11.363C13.8483 10.9233 13.4919 10.5644 13.0486 10.5654C12.5944 10.5754 12.239 10.9452 12.24 11.405ZM13.0555 15.8923C12.6013 15.8823 12.235 15.5035 12.234 15.0437C12.2241 14.584 12.5885 14.2032 13.0426 14.1922H13.0525C13.5165 14.1922 13.8927 14.571 13.8927 15.0407C13.8937 15.5105 13.5185 15.8913 13.0555 15.8923ZM8.17211 11.4201C8.19186 11.8799 8.56803 12.2387 9.0222 12.2187C9.4665 12.1978 9.82095 11.8179 9.80121 11.3582C9.79035 10.9084 9.42503 10.5586 8.98074 10.5596C8.52657 10.5796 8.17113 10.9604 8.17211 11.4201ZM9.02623 15.8476C8.57206 15.8676 8.19687 15.5088 8.17614 15.049C8.17614 14.5893 8.53059 14.2095 8.98476 14.1885C9.42906 14.1875 9.79536 14.5373 9.80523 14.9861C9.82597 15.4468 9.47053 15.8267 9.02623 15.8476ZM4.10434 11.4555C4.12409 11.9153 4.50026 12.2751 4.95443 12.2541C5.39873 12.2341 5.75318 11.8533 5.73245 11.3936C5.72257 10.9438 5.35726 10.594 4.91198 10.595C4.45781 10.615 4.10336 10.9958 4.10434 11.4555ZM4.95836 15.8525C4.50419 15.8735 4.12901 15.5137 4.10827 15.0539C4.10728 14.5942 4.46272 14.2133 4.91689 14.1934C5.36119 14.1924 5.72749 14.5422 5.73736 14.992C5.7581 15.4517 5.40365 15.8325 4.95836 15.8525Z" fill="#D3D3D3"/>
</svg>

{{card.orderDate}}
      </v-col>
      <v-col class="">
<svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
<path fill-rule="evenodd" clip-rule="evenodd" d="M5.66991 9.91821e-05H14.3399C17.7299 9.91821e-05 19.9999 2.3791 19.9999 5.9191V14.0891C19.9999 17.6201 17.7299 20.0001 14.3399 20.0001H5.66991C2.27991 20.0001 -9.15527e-05 17.6201 -9.15527e-05 14.0891V5.9191C-9.15527e-05 2.3791 2.27991 9.91821e-05 5.66991 9.91821e-05ZM13.5799 13.8101C13.8299 13.8101 14.0799 13.6801 14.2199 13.4401C14.4399 13.0891 14.3199 12.6291 13.9599 12.4101L10.3999 10.2901V5.6691C10.3999 5.2601 10.0699 4.9191 9.64991 4.9191C9.23991 4.9191 8.89991 5.2601 8.89991 5.6691V10.7201C8.89991 10.9801 9.03991 11.2301 9.26991 11.3601L13.1899 13.7001C13.3099 13.7801 13.4499 13.8101 13.5799 13.8101Z" fill="#D3D3D3"/>
</svg>
{{card.orderDate}}
      </v-col>
     </v-row>
      <v-card-text >
        <v-card-title>Получатель:</v-card-title>
        <v-card-subtitle class="">{{card.account}}</v-card-subtitle>
        <v-card-title>Адрес:</v-card-title>
       <v-card-subtitle class="">{{card.address}}</v-card-subtitle>
      </v-card-text>
      <v-card-actions>
        <v-btn color="#6A65FF"  elevation="2" text width="100%">Забрать по QR</v-btn>
      </v-card-actions>
      </v-card>
 </v-container>
      
           <v-pagination v-model="currentPage" :value="currentPage" @input="addItems()" :length="allPages"></v-pagination>
    </v-container>
  </v-main>

  <v-footer app>

  </v-footer>
</v-app>
</template>

<script>
import axios from 'axios'

export default {
name: 'App',
components:{

},
data(){
 return {
  items:null,
  typeDelivery: "completed",
  currentPage:1,
  allPages:null,
 }
},
methods:{
  addItems(){  
    this.items = []
     axios.post(
  'https://api2.wbprod.ru/v1/deliverys/get',
  {
   "type":this.typeDelivery,
   "page":this.currentPage
},
   {
    headers: {
      wb_client_id: 1
    },
  }
  )
  .then(resp=>{
    console.log(resp)
    this.items = resp.data.data.data
    this.allPages = resp.data.data.pages
  });
  }
},
mounted(){
this.addItems()


}
};
</script>
