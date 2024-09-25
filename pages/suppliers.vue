<template>
    <Snackbar :open="snackbarOpen" :message="snackbarNote" :success="snackbarSuccess">
        <div @click="snackbarOpen=false"  class="hover:cursor-pointer flex w-fit align-middle justify-center font-bold text-red-700">close</div>
    </Snackbar>
    <Popup v-if="supplierUpdate || supplierPassword || addSupplier">
        <div v-if="dialogError!=null" class="w-full h-7 text-white flex justify-center bg-red-600">
            {{ dialogError }}
        </div>
        <!-- <div v-if="supplierUpdate">
            <form @submit.prevent="updateSupplier">
                <div class="py-4">
                    <label class="block pb-2" for="fn">Company Name</label>
                    <input @input="dialogError=null" v-model="updateCname" class="border-2 border-gray-600 rounded-md" id="fn" type="text">
                </div>
                <div v-if="false" class="py-4">
                    <label  class="block pb-2" for="e">Email</label>
                    <input @input="dialogError=null" v-model="updateEmail"  class="border-2 border-gray-600 rounded-md" id="e" type="email">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="pn">Phone No</label>
                    <input @input="dialogError=null" v-model="updatePhoneNo"  class="border-2 border-gray-600 rounded-md" id="pn" type="tel">
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white py-2 px-6 rounded-full" @click="updateSupplier">Update</button>
                    <button @click="supplierUpdate=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
            </form>
        </div> -->
        <div v-if="supplierPassword">
            <form  @submit.prevent="changePassword">
                <div v-if="false" class="py-4">
                    <label class="block pb-2" for="pas">Password</label>
                    <input @input="dialogError=null" class="border-2 border-gray-600 rounded-md" id="pas" type="password">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="new_pas">New password</label>
                    <input @input="dialogError=null" v-model="newPassword" class="border-2 border-gray-600 rounded-md" id="new_pas" type="password">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="con_pas">Confirm password</label>
                    <input @input="dialogError=null" v-model="confirmPassword"  class="border-2 border-gray-600 rounded-md" id="con_pas" type="password">
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white p-2 rounded-full" @click="changePassword">Change password</button>
                    <button @click="supplierPassword=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
                
            </form>
        </div>
        <div v-if="addSupplier">
            <form  @submit.prevent="createSupplier">
                <div class="py-4">
                    <label class="block pb-2" for="fn">Company Name</label>
                    <input @input="dialogError=null" v-model="Cname" class="border-2 border-gray-600 rounded-md" id="fn" type="text">
                </div>
                
                <div class="py-4">
                    <label  class="block pb-2" for="e">Email</label>
                    <input @input="dialogError=null" v-model="Email"  class="border-2 border-gray-600 rounded-md" id="e" type="email">
                </div>
                
                <div class="py-4">
                    <label  class="block pb-2" for="p">Password</label>
                    <input @input="dialogError=null" v-model="Password"  class="border-2 border-gray-600 rounded-md" id="p" type="password">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="cp">Confirm Password</label>
                    <input @input="dialogError=null" v-model="Cpassword"  class="border-2 border-gray-600 rounded-md" id="cp" type="password">
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white py-2 px-6 rounded-full" @click="createSupplier">Add Supplier</button>
                    <button @click="addSupplier=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
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

                <button @click="addSupplier=true" class=" text-white  bg-indigo-950 rounded-md flex text-center px-4 py-2 mb-2 mr-6">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
                    </svg>
                    Add 
                </button>


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
                    <li class="w-48 text-center p-2">Company name</li>
                    <li class="w-48 text-center p-2">Email</li>
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

            <div v-else-if="searchData!=null" v-for="(item,index) in searchData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.company_name }}</li>
                    <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.email }}</li>
                    <li :class="{'text-red-600':item.status.manager=='pending','text-green-600':item.status.manager=='approved'}" class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.status.manager }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>
                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2 hover:cursor-pointer" @click="supplierApprove(item.id)" >approve</li>
                            <!-- <li class="py-2 hover:cursor-pointer" @click="supplierUpdate=true; popItemId=item.id">update</li> -->
                            <li class="py-2 hover:cursor-pointer" @click="supplierPassword=true; popItemId=item.id">change password</li>
                            <li class="py-2 hover:cursor-pointer" @click="supplierDelete(item.id)">delete</li>
                        </ul>
                    </div>
                    </li>
                </ul> 
                 
            </div>

            
            <div v-else v-for="(item,index) in onlyPending? pendingData : myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.company_name }}</li>
                    <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.email }}</li>
                    <li :class="{'text-red-600':item.status.manager=='pending','text-green-600':item.status.manager=='approved'}" class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.status.manager }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>
                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2 hover:cursor-pointer" @click="supplierApprove(item.id)" >approve</li>
                            <!-- <li class="py-2 hover:cursor-pointer" @click="supplierUpdate=true; popItemId=item.id">update</li> -->
                            <li class="py-2 hover:cursor-pointer" @click="supplierPassword=true; popItemId=item.id">change password</li>
                            <li class="py-2 hover:cursor-pointer" @click="supplierDelete(item.id)">delete</li>
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
const addSupplier=ref(false);
const dialogError=ref(null);

const snackbarNote=ref(null);
const snackbarOpen=ref(false);
const snackbarSuccess=ref(true);

const myData=ref(null);
const searchData=ref(null);
const pendingData=ref([]);
const searchQuery=ref(null);

const onlyPending= ref(false);
const supplierUpdate=ref(false);
const supplierPassword=ref(false);
const popItemId=ref(null);

const newPassword=ref(null);
const confirmPassword=ref(null);

const Cname=ref(null);
const Email=ref(null);
const Password=ref(null);
const Cpassword=ref(null);

onMounted(()=>{refresh()})

async function search() {
    if (!searchQuery) {
        return;
    }

    const data= await $fetch('http://165.22.123.187/api/search-supplier',
        {
            method:'GET',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            params:{search:searchQuery.value},
            onResponse({response}){
                if (response.status==200) {
                    searchData.value=response._data.data;
                }else{
                    console.log(response._data)
                }
                
            }
        }
    )
}


async function supplierApprove(id) {
    if (!confirm('confirm this approve action')) {
        return;
    }

    const data =await $fetch('http://165.22.123.187/api/approve-suppliers',
        {
            method:'POST',
            params:{id:id},
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    refresh();
                    snackbarNote.value='Approved successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true;
                }
            }
        }
    )
}

async function createSupplier() {
    dialogStatus.value=false;
    if (Cname&&Email&&Password) {
        if (Password.value!=Cpassword.value) {
            dialogError.value='wrong confirmation';
            return;
        }else if (Password.value.length<8) {
            dialogError.value='too short password';
            return;
        }
    }else{
        dialogError.value='all fields are required';
        return;
    }

    const params={
        company_name:Cname.value,
        email:Email.value,
        password:Password.value,
    }
    const data= await $fetch('http://165.22.123.187/api/suppliers',
        {
            method:'POST',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            params:params,
            onResponse({response}){
                if (response.status>=200 && response.status<300) {
                    supplierUpdate.value=false;
                    dialogError.value=null;
                    addSupplier.value=false;
                    refresh();
                    snackbarNote.value='password update successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true;
                }else{
                dialogError.value=response._data.message;
            }
                
            }
        }
    )
}

async function changePassword() {
    dialogStatus.value=false;
    if (confirmPassword.value!=null && newPassword.value!=null) {
        if (newPassword.value!=confirmPassword.value) {
            dialogError.value='wrong confirmation';
            return;
        }
        if (newPassword.value.length<8) {
            dialogError.value='your password is too short';
            return;
        }
        const data = await $fetch('http://165.22.123.187/api/update-sup-password',
            {
                method:'POST',
                headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
                params:{
                    id:popItemId.value,
                    password:newPassword.value,
                }
                ,
                onResponse({response,}){
                    if (response.status==200) {
                        supplierPassword.value=false;
                        dialogError.value=null;
                        snackbarNote.value='password update successfully';
                        snackbarSuccess.value=true;
                        snackbarOpen.value=true;
                    }
                },
            }
        )
    }else{
        dialogError.value='all fields are required';
        return;
    }
    
}


async function supplierDelete(id) {
    if (!confirm('confirm this delete action')) {
        return;
    }

    const data= await $fetch('http://165.22.123.187/api/suppliers/'+id,
        {
            method:'DELETE',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if (response.status==200) {
                    refresh();
                    snackbarNote.value='Supplier deleted successfully';
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

const { data, status ,pending, error, refresh } = await useFetch('http://165.22.123.187/api/suppliers',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            if (response.status==200) {
                myData.value=response._data.data;
                response._data.data.forEach(element => {
                    if (element.status.manager=='pending') {
                        pendingData.value.push(element);
                    }
                });
            }
        }
    }
)

</script>