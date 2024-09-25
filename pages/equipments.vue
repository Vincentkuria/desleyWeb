<template>
    <Snackbar :open="snackbarOpen" :message="snackbarNote" :success="snackbarSuccess">
        <div @click="snackbarOpen=false"  class="hover:cursor-pointer flex w-fit align-middle justify-center font-bold text-red-700">close</div>
    </Snackbar>
    <Popup v-if="equipmentUpdate || addEquipment">
        <div v-if="dialogError!=null" class="w-full h-7 text-white flex justify-center bg-red-600">
            {{ dialogError }}
        </div>
        <div v-if="equipmentUpdate">
            <form  @submit.prevent enctype="multipart/form-data">
                <div class="py-4">
                    <label class="block pb-2" for="n">Name</label>
                    <input @input="dialogError=null" v-model="updateName" class="border-2 border-gray-600 rounded-md" id="n" type="text">
                </div>
                <div class="py-4">
                    <label class="block pb-2" for="d">Description</label>
                    <textarea @input="dialogError=null" v-model="updateDescription" class="border-2 border-gray-600 rounded-md" id="d" type="text"></textarea>
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="p">Price</label>
                    <input @input="dialogError=null" v-model="updatePrice"  class="border-2 border-gray-600 rounded-md" id="p" type="number">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="i">Image</label>
                    <input @change="(f)=>{updateImg=f.target.files[0]}"  class="border-2 border-gray-600 rounded-md" id="i" type="file" accept="image/*" >
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white py-2 px-6 rounded-full" @click="updateEquipment">Update</button>
                    <button @click="equipmentUpdate=false; dialogError=null" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
            </form>
        </div>

        <div v-if="addEquipment">
            <form  @submit.prevent  enctype="multipart/form-data">
                <div class="py-4">
                    <label class="block pb-2" for="n">Name</label>
                    <input @input="dialogError=null" v-model="Name" class="border-2 border-gray-600 rounded-md" id="n" type="text">
                </div>
                <div class="py-4">
                    <label class="block pb-2" for="d">Description</label>
                    <textarea @input="dialogError=null" v-model="Description" class="border-2 border-gray-600 rounded-md" id="d" type="text"></textarea>
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="p">Price</label>
                    <input @input="dialogError=null" v-model="Price"  class="border-2 border-gray-600 rounded-md" id="p" type="number">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="i">Image</label>
                    <input @change="(f)=>{Image=f.target.files[0]}" class="border-2 border-gray-600 rounded-md" id="i" type="file" accept="image/*" >
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="inv">Inventory</label>
                    <div @click="invMenuOpen ? invMenuOpen =false :invMenuOpen=true;" id="inv" class=" p-3 border-2 border-indigo-950 rounded-lg text-indigo-950">{{ invSelected? allInv[invSelectedIndex].name:'Select' }}</div>
                    <div class="relative w-full h-0">
                        <ul v-if="invMenuOpen" ref="invItem" class="absolute max-h-64 overflow-y-scroll top-0 left-4 bg-slate-100 text-indigo-950 shadow-2xl z-10 p-4">
                            <li v-for="(item,index) in allInv" @click="invSelected=item.id; invSelectedIndex=index; invMenuOpen=false" class="py-2 hover:cursor-pointer" >{{ item.name }}</li>
                        </ul>
                    </div>
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white py-2 px-6 rounded-full" @click="createEquipment()">Create Equipment</button>
                    <button @click="addEquipment=false; dialogError=null; cleardata()" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
            </form>
        </div>
        
    </Popup>
    <div class="h-screen">
        <div class="h-1/5">

            <div class="h-1/3 w-full flex shadow-2xl">
                <div class="w-full h-full flex pb-1 ms-7">
                    
                    <input v-model="searchQuery" class="w-1/2 border-2 px-2 rounded-lg border-indigo-950" type="text" placeholder="Search" >
                    <button @click="search"  class="bg-indigo-950 text-white mx-2 p-2 px-4 rounded-full">
                        
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
                        </svg>

                    </button>
                </div>

                <button @click="addEquipment=true;" class=" text-white  bg-indigo-950 rounded-md flex text-center px-4 py-2 mb-2 mr-6">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
                    </svg>
                    Add 
                </button>
            </div>

            <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center p-2">Equipment</li>
                    <li class="w-28 text-center p-2">Price</li>
                    <li class="w-52 text-center p-2">Description</li>
                    <li class="w-28 text-center p-2">Image</li>
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

            <div v-else v-for="(item,index) in myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.name }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.price }}</li>
                    <li class="w-52 h-24 text-center py-1 px-2 overflow-y-scroll">{{ item.item_description }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden"><img height="6rem" class="object-contain" :src="item.img_url"></li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>

                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li v-if="false" class="py-2 hover:cursor-pointer" @click="equipmentUpdate=true; popItemId=item.id">update</li>
                            <li class="py-2 hover:cursor-pointer" @click="deleteEquipment(item.id)">delete</li>
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
const popItemId=ref(null);
const addEquipment=ref(false);
const dialogError=ref(null);

const myData=ref(null);

const equipmentUpdate=ref(null);

const snackbarNote=ref(null);
const snackbarOpen=ref(false);
const snackbarSuccess=ref(true);

const searchQuery=ref(null);
const searchData=ref(null);

const invItem=ref(null);
const invMenuOpen=ref(false);
const invSelected=ref(null);
const invSelectedIndex=ref(null);

const updateName=ref(null);
const updateDescription=ref(null);
const updatePrice=ref(null);
const updateImg=ref(null);

const Name=ref(null);
const Description=ref(null);
const Price=ref(null);
const Image=ref(null);

const allInv=ref([]);


const { data, status,pending, error, refresh, clear } = await useFetch('http://165.22.123.187/api/equipments',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            myData.value=response._data.data;
        }
    }
)

onMounted(()=>{
    refresh();
    getInventory();
})

function cleardata(){
    Name.value=null;
    Description.value=null;
    Price.value=null;
    Image.value=null;
    invSelected.value=null;
}

async function getInventory() {
    const data = await $fetch('http://165.22.123.187/api/inventories',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            if (response.status==200) {

                response._data.data.forEach(element => {
                    if (element.supplier!=null) {
                        allInv.value.push(element);
                    }
                });
                // myData.value=response._data.data;
            }
        }
    }
)
}

async function createEquipment() {
    dialogError.value=null;
    if (Name.value!=null&&Description.value!=null&&Price.value!=null&&Image.value!=null) {
        
    } else {
        dialogError.value='all fields are required';
        return;
    }

    const params=new FormData();
    params.append('name',Name.value);
    params.append('item_description',Description.value);
    params.append('price',Price.value);
    params.append('img',Image.value);
    params.append('inventory_id',invSelected.value);

        
    const data = await $fetch('http://165.22.123.187/api/equipments',
        {
            method:'POST',
            body:params,
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    addEquipment.value=false;
                    refresh();
                    snackbarNote.value='equipment added successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true
                    cleardata();

                }
            }

        }
    )
}

async function deleteEquipment(id) {
    if (!confirm('confirm this delete action')) {
        return;
    }
    
    const data = await useFetch('http://165.22.123.187/api/equipments/'+id,
        {
            method:'DELETE',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    refresh();
                    snackbarNote.value='equipment deleted successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true;
                }
            }
        }
    )
}

async function updateEquipment() {
    dialogError.value=null;
    if (updateName.value!=null&&updateDescription.value!=null&&updatePrice.value!=null&&updateImg.value!=null) {
        
    }else{
        dialogError.value='all fields are required';
        return;
    }

    const params=new FormData();
    params.append('name',updateName.value);
    params.append('item_description',updateDescription.value);
    params.append('price',updatePrice.value);
    params.append('img',updateImg.value);

        
    const data = await $fetch('http://165.22.123.187/api/equipments/'+popItemId.value,
        {
            method:'PATCH',
            body:params,
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    addEquipment.value=false;
                    refresh();
                    snackbarNote.value='equipment updated successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true

                }else{
                    console.log(response._data)
                }
            }

        }
    )

}

onClickOutside(popupItem, () => {
    dialogStatus.value=false;
})

onClickOutside(invItem, () => {
    invMenuOpen.value=false;
})

</script>