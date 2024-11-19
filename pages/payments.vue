<template>
    <Snackbar :open="snackbarOpen" :message="snackbarNote" :success="snackbarSuccess">
        <div @click="snackbarOpen=false"  class="hover:cursor-pointer flex w-fit align-middle justify-center font-bold text-red-700">close</div>
    </Snackbar>
    
    <div class="h-screen">
        <div class="h-1/5">
            
            <div class="h-1/3 w-full flex shadow-2xl">
                <div class="w-full h-full flex pb-1 ms-7">
                    
                    <input v-model="searchQuery" class="w-1/2 border-2 px-2 rounded-lg border-indigo-950" type="text" placeholder="Search" >
                    <button @click="search();hello()"  class="bg-indigo-950 text-white mx-2 p-2 px-4 rounded-full">
                        
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
                        </svg>

                    </button>
                </div>

                <div class="w-44 flex h-5/6 mr-4 border-indigo-950 border-2">
                    <button @click="onlyPending=false; searchData=null; searchQuery=null " :class="{'bg-indigo-950':!onlyPending, 'text-white':!onlyPending}" class="w-1/2 h-full flex justify-center align-middle">
                        All
                    </button>
                    <button @click="onlyPending=true" :class="{'bg-indigo-950':onlyPending, 'text-white':onlyPending}" class="w-1/2 h-full align-middle flex justify-center">
                        Pending
                    </button>
                </div>
            </div>

            <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center p-2">Code</li>
                    <li class="w-28 text-center p-2">Customer</li>
                    <li class="w-28 text-center p-2">Amount</li>
                    <li class="w-28 text-center p-2">Status</li>
                    <li class="w-28 text-center p-2">Date created</li>
                    <li class="w-28 text-center p-2">Last updated</li>
                    <li class="w-28 text-center p-2"><!--for alignment purposes--></li>
                </ul>
            </div>
        </div>
        

        <div class="h-4/5 overflow-scroll">
            <div v-if="pending">
                Loading......
            </div>

            <div v-else-if="searchData!=null && searchData.length!=0" v-for="(item,index) in searchData"  class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis text-nowrap">{{ item.payment_code }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.customer.first_name+' '+item.customer.last_name }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.amount }}</li>
                    <li :class="{'text-red-600':item.status.finance=='pending','text-green-600':item.status.finance=='approved'}"  class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.status.finance }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>
                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2 hover:cursor-pointer" @click="paymentApprove(item.id)" >approve</li>
                            <li class="py-2 hover:cursor-pointer" @click="paymentDelete(item.id)">delete</li>
                        </ul>
                    </div>
                    </li>
                </ul> 
                 
            </div>
            
            <div v-else v-for="(item,index) in onlyPending ? pendingData : myData"  class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis text-nowrap">{{ item.payment_code }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.customer.first_name+' '+item.customer.last_name }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.amount }}</li>
                    <li :class="{'text-red-600':item.status.finance=='pending','text-green-600':item.status.finance=='approved'}"  class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.status.finance }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>
                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2 hover:cursor-pointer" @click="paymentApprove(item.id)" >approve</li>
                            <li class="py-2 hover:cursor-pointer" @click="paymentDelete(item.id)">delete</li>
                        </ul>
                    </div>
                    </li>
                </ul> 
                 
            </div>
        </div>
        
    </div>
</template>

<script setup>
const dialogStatus=ref(false);
const dialogNo=ref(null);
const popupItem=ref(null);
const onlyPending=ref(false);

const snackbarNote=ref(null);
const snackbarOpen=ref(false);
const snackbarSuccess=ref(true);


const myData=ref([]);
const pendingData=ref([]);
const searchData=ref([]);
const searchQuery=ref(null);

onMounted(()=>{
    myData.value=[];
    pendingData.value=[];
    refresh()

})

const {data, status,pending, error, refresh, clear } =await useFetch('http://138.68.154.175/api/payments',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            if (response.status==200) {
                // myData.value=response._data.data;
                response._data.data.forEach(element => {
                    if (element.customer!=null) {
                        myData.value.push(element);
                        if (element.status.finance=='pending') {
                        pendingData.value.push(element);
                    }
                    }
                    
                });

            }
        }
    }
)

function hello() {
    console.log(myData.value.length);
    console.log(pendingData.value.length);
    console.log(searchData.value.length);
    console.log(onlyPending.value);
}

async function search() {
    if (searchQuery.value==null) {
        return;
    }
    console.log(searchQuery.value);
    const data= await $fetch('http://138.68.154.175/api/search-payment-code',
        {
            method:'GET',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            params:{search:searchQuery.value},
            onResponse({response}){
                searchData.value=[];
                response._data.data.forEach(element => {
                    if (element.customer!=null) {
                        searchData.value.push(element);
                    }
                    
                });
            }
        }
    )
}

async function paymentApprove(id) {
    if (!confirm('confirm this approve action')) {
        return;
    }

    const data =await $fetch('http://138.68.154.175/api/approve-payment',
        {
            method:'POST',
            params:{id:id},
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    myData.value=[];
                    pendingData.value=[];
                    refresh();
                    snackbarNote.value='Approved successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true;
                }
            }
        }
    )
}

async function paymentDelete(id) {
    if (!confirm('confirm this delete action')) {
        return;
    }
    const data= await $fetch('http://138.68.154.175/api/payments/'+id,
        {
            method:'DELETE',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    myData.value=[];
                    pendingData.value=[];
                    refresh();
                    snackbarNote.value='Payment deleted successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true;
                }
            }

        }
    )
}

onClickOutside(popupItem, () => {
    dialogStatus.value=false;
})

</script>