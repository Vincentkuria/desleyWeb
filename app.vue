<template>
  <div class="w-screen h-screen p-4 flex">
      <div class="w-1/5 h-full shadow-2xl z-10">
          <div class="justify-items-center  flex w-full p-2">
              <img src="assets/images.png" class="m-auto object-contain w-20 h-20"  >
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
onMounted(()=>{
    console.log(route.path)
})
</script>