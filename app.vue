<template>
    <NuxtLoadingIndicator color="#1e1b4b"/>
    <form v-if="token==null" @submit.prevent="submit" class="h-screen w-screen">
        <div class="after:content-['Desley'] after:m-auto after:content-center after:justify-center after:flex after:font-bold after:text-indigo-950 text-lg">
            <img src="./assets/images.png" class="object-contain w-24 pt-10 pb-2 m-auto">
        </div>

        <h1 class="justify-center text-4xl flex p-16 font-bold">Admin</h1>

        <div class="flex m-auto justify-items-center">
            <div class="m-auto w-1/3">
                <label class="block pb-2" for="fn">Password</label>
                <input v-model="adminPassword" @input="loginError=null" class="border-2 border-gray-600 rounded-md p-4 w-full" id="fn" type="password">
            </div> 
        </div>
        <div v-if="loginError" class="text-red-700 flex justify-center">
            {{ loginError}}
        </div>

        <div class="flex justify-items-center">
            <button @click="submit" class="mx-auto my-4 rounded-xl p-5 w-1/3 text-white bg-indigo-950">
                Login
            </button>
        </div>
    </form>


  <div v-else class="w-screen h-screen p-4 flex">
      <div class="w-1/5 h-full shadow-2xl z-10">
          <div class="justify-items-center  flex w-full p-2">
              <img src="assets/images.png" class="m-auto object-contain w-20 h-20">
          </div>
          <div>
              <ul class="text-indigo-950 text-center py-5">
                  <li :class="{'text-white':currentPage==0, 'bg-indigo-950':currentPage==0}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=0" to="/">Customers</NuxtLink>  </li>
                  <li :class="{'text-white':currentPage==1, 'bg-indigo-950':currentPage==1}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=1" to="/employees">Employees</NuxtLink></li>
                  <li :class="{'text-white':currentPage==2, 'bg-indigo-950':currentPage==2}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=2" to="/payments">Payments</NuxtLink>  </li>
                  <li :class="{'text-white':currentPage==3, 'bg-indigo-950':currentPage==3}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=3" to="/shippings">Shippings</NuxtLink>  </li>
                  <li :class="{'text-white':currentPage==4, 'bg-indigo-950':currentPage==4}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=4" to="/inventories">Inventories</NuxtLink>  </li>
                  <li :class="{'text-white':currentPage==5, 'bg-indigo-950':currentPage==5}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=5" to="/equipments">Equipments</NuxtLink>  </li>
                  <li :class="{'text-white':currentPage==6, 'bg-indigo-950':currentPage==6}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=6" to="/spares">Spares</NuxtLink>  </li>
                  <li :class="{'text-white':currentPage==7, 'bg-indigo-950':currentPage==7}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=7" to="/services">Services</NuxtLink>  </li>
                  <li :class="{'text-white':currentPage==8, 'bg-indigo-950':currentPage==8}" class="p-3 hover:cursor-pointer"><NuxtLink @click="currentPage=8" to="/suppliers">Suppliers</NuxtLink>  </li>
              </ul>
          </div>
      </div>
      <div class="w-full h-full pl-4">
<NuxtPage/>
      </div>
      
  </div>
</template>

<script setup>
//set current page onmount
const currentPage=ref(0);
const route=useRoute();
const adminPassword=ref(null);
const loginError=ref(null);
const token=ref(null)

async function submit() {
    
    if (!adminPassword.value) {
        loginError.value="password filled required";
        return 
    }

    const data= await $fetch('http://165.22.123.187/api/elogin',
        {
            method:'POST',
            body:{email:'admin@desley.com', password:adminPassword.value},
            onResponse({response}){
                if (response.status==200) {
                    localStorage.setItem('token',response._data.data.token);
                token.value=localStorage.getItem('token');
                }else{
                    loginError.value=response._data.message
                }
                
            },
            onRequestError({error}){
                loginError.value=error.message;
            },
            onResponseError({request,response,options}){
                loginError.value=response._data.message;
            }
        }
    )

    
}

onMounted(()=>{
    token.value=localStorage.getItem('token');
    switch (route.path) {
        case '/employees':currentPage.value=1; break;
        case '/payments':currentPage.value=2; break;
        case '/shippings':currentPage.value=3; break;
        case '/inventories': currentPage.value=4; break;
        case '/equipments': currentPage.value=5; break;
        case '/spares': currentPage.value=6; break;
        case '/services': currentPage.value=7; break;
        case '/suppliers': currentPage.value=8; break;
        default:currentPage.value=0; break;
    }
})
</script>