<template>
    <Popup v-if="false">
        <div v-for="x in 20">Hello kenya Hello kenya Hello kenya Hello kenya Hello kenya</div>
    </Popup>
    <div class="h-screen">
        <div class="h-1/5">
            
            <div class="h-1/3 w-full flex shadow-2xl">
                <div class="w-full h-full flex pb-1 ms-7">
                    
                    <input @input="inputchange" v-model="searchQuery" class="w-1/2 border-2 px-2 rounded-lg border-indigo-950" type="text" placeholder="Search" >
                    <button @click="search"  class="bg-indigo-950 text-white mx-2 p-2 px-4 rounded-full">
                        
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
                        </svg>

                    </button>
                </div>
            </div>
            
            <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center p-2">Item</li>
                    <li class="w-28 text-center p-2">Count</li>
                    <li class="w-28 text-center p-2">Supplier</li>
                    <li class="w-28 text-center p-2">Date created</li>
                    <li class="w-28 text-center p-2">Last updated</li>
                    <!-- <li class="w-28 text-center p-2">for alignment purposes</li> -->
                </ul>
            </div>
        </div>
        

        <div class="h-4/5 overflow-scroll">
            <div v-if="pending">
                Loading......
            </div>

            <div v-else-if="searchData" v-for="(item,index) in searchData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.name }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.no_of_items }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.supplier.company_name }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <!-- <li class="w-28 text-center py-1 px-2">
                        <svg  @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>
                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2">update</li>
                            <li class="py-2">delete</li>
                        </ul>
                    </div>
                    </li> -->
                </ul> 
                 
            </div>

            <div v-else v-for="(item,index) in myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.name }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.no_of_items }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.supplier.company_name }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <!-- <li class="w-28 text-center py-1 px-2">
                        <svg  @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>
                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2">update</li>
                            <li class="py-2">delete</li>
                        </ul>
                    </div>
                    </li> -->
                </ul> 
                 
            </div>
        </div>
        
    </div>
</template>

<script setup>
const dialogStatus=ref(false);
const dialogNo=ref(null);
const popupItem=ref(null);

const myData=ref([]);
const searchData =ref(null);
const searchQuery=ref(null);

onClickOutside(popupItem, () => {
    dialogStatus.value=false;
})

onMounted(()=>{
    myData.value=[];
    refresh();
})

const inputchange=()=>{
    if (searchQuery.value) {
        return;
    } else {
        searchData.value=null;
    }
}
const {data, status,pending, error, refresh, clear } =await useFetch('http://164.90.212.129/api/inventories',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            if (response.status==200) {

                response._data.data.forEach(element => {
                    if (element.supplier!=null) {
                        myData.value.push(element);
                    }
                });
                // myData.value=response._data.data;
            }
        }
    }
)

async function search() {
    if (!searchQuery) {
        return;
    }

    const data = await $fetch('http://164.90.212.129/api/inventory-search',
        {
            method:'GET',
            params:{search:searchQuery.value},
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    searchData.value=response._data.data;
                }
            }
        }
    )
}


</script>