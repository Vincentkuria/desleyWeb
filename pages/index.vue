<template>
    <Snackbar :open="snackbarOpen" :message="snackbarNote" :success="snackbarSuccess">
        <div @click="snackbarOpen=false"  class="hover:cursor-pointer flex w-fit align-middle justify-center font-bold text-red-700">close</div>
    </Snackbar>
    <Popup v-if="customerUpdate || customerPassword || addCustomer ">
        <div v-if="dialogError!=null" class="w-full h-7 text-white flex justify-center bg-red-600">
            {{ dialogError }}
        </div>
        <div v-if="customerUpdate">
            <form  @submit.prevent="updateCustomer">
                <div class="py-4">
                    <label class="block pb-2" for="fn">First Name</label>
                    <input @input="dialogError=null" v-model="updateFname" class="border-2 border-gray-600 rounded-md" id="fn" type="text">
                </div>
                <div class="py-4">
                    <label class="block pb-2" for="ln">Last Name</label>
                    <input @input="dialogError=null" v-model="updateLname" class="border-2 border-gray-600 rounded-md" id="ln" type="text">
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
                    <button class=" bg-indigo-950 text-white py-2 px-6 rounded-full" @click="updateCustomer">Update</button>
                    <button @click="customerUpdate=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
            </form>
        </div>
        <div v-if="customerPassword">
            <form @submit.prevent="changePassword">
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
                    <button @click="customerPassword=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
                
            </form>
        </div>

        <div v-if="addCustomer">
            <form  @submit.prevent="createCustomer">
                <div class="py-4">
                    <label class="block pb-2" for="fn">First Name</label>
                    <input @input="dialogError=null" v-model="Fname" class="border-2 border-gray-600 rounded-md" id="fn" type="text">
                </div>
                <div class="py-4">
                    <label class="block pb-2" for="ln">Last Name</label>
                    <input @input="dialogError=null" v-model="Lname" class="border-2 border-gray-600 rounded-md" id="ln" type="text">
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
                <div class="py-4">
                    <label  class="block pb-2" for="pn">Phone No</label>
                    <input @input="dialogError=null" v-model="PhoneNo"  class="border-2 border-gray-600 rounded-md" id="pn" type="tel">
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white py-2 px-6 rounded-full" @click="createCustomer">Create customer</button>
                    <button @click="addCustomer=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
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

                <button @click="addCustomer=true" class=" text-white  bg-indigo-950 rounded-md flex text-center px-4 py-2 mb-2 mr-6">
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
                <svg @click="logMeOut" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 my-auto mr-5  text-red-600">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M5.636 5.636a9 9 0 1 0 12.728 0M12 3v9" />
                </svg>

            </div>


            <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center p-2">Name</li>
                    <li class="w-48 text-center p-2">Email</li>
                    <li class="w-28 text-center p-2">Phone No</li>
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

            <div v-else-if="searchData!==null"  v-for="(item,index) in searchData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.first_name+item.last_name }}</li>
                    <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.email }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.phone_no }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis" :class="{'text-red-600':!item.verified, 'text-green-600':item.verified }">{{ item.verified ? 'approved' :'pending' }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>

                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2 hover:cursor-pointer" @click="approveCustomer(item.id,index)">approve</li>
                            <li class="py-2 hover:cursor-pointer" @click="customerUpdate=true; popItemId=item.id">update</li>
                            <li class="py-2 hover:cursor-pointer" @click="customerPassword=true; popItemId=item.id">change password</li>
                            <li class="py-2 hover:cursor-pointer" @click="deleteCustomer(item.id)">delete</li>
                        </ul>
                    </div>
                    </li>
                </ul> 
                 
            </div>
            
            <div v-else  v-for="(item,index) in onlyPending? pendingData : myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.first_name+item.last_name }}</li>
                    <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.email }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.phone_no }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis" :class="{'text-red-600':!item.verified, 'text-green-600':item.verified }">{{ item.verified ? 'approved' :'pending' }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.updated_at }}</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true; dialogNo=item" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>

                    <div class="relative w-0 h-0">
                        <ul v-if="dialogStatus && dialogNo==item" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2 hover:cursor-pointer" @click="approveCustomer(item.id,index)">approve</li>
                            <li class="py-2 hover:cursor-pointer" @click="customerUpdate=true; popItemId=item.id">update</li>
                            <li class="py-2 hover:cursor-pointer" @click="customerPassword=true; popItemId=item.id">change password</li>
                            <li class="py-2 hover:cursor-pointer" @click="deleteCustomer(item.id)">delete</li>
                        </ul>
                    </div>
                    </li>
                </ul> 
                 
            </div>
        </div>
        
    </div>
</template>

<script setup>
const customerUpdate=ref(false);
const customerPassword=ref(false);
const dialogStatus=ref(false);
const dialogNo=ref(null);
const popupItem=ref(null);
const myData=ref(null);
const pendingData=ref([]);
const onlyPending=ref(false);
const searchQuery=ref(null);
const searchData=ref(null);

//update
const updateFname=ref(null);
const updateLname=ref(null);
const updateEmail=ref(null);
const updatePhoneNo=ref(null);
const popItemId=ref(null);

//password
const newPassword=ref(null);
const confirmPassword=ref(null);

const snackbarNote=ref(null);
const snackbarOpen=ref(false);
const snackbarSuccess=ref(true);

const dialogError=ref(null);

//add
const addCustomer=ref(false);
const Fname=ref(null);
const Lname=ref(null);
const Email=ref(null);
const Password=ref(null);
const Cpassword=ref(null);
const PhoneNo=ref(null);

async function createCustomer() {
    if (Fname.value && Lname.value && Email.value && Password.value && Cpassword.value && PhoneNo.value) {
        if (Password.value!=Cpassword.value) {
            dialogError.value='please confirm password correctly';
            return;
        }else if(Password.value.length<8){
            dialogError.value='your password is too short';
            return;
        }

        if (PhoneNo.value.length<10) {
            dialogError.value='wrong phone number';
            return;
        }
    }else{
        dialogError.value='all fields are required';
        return;
    }

    const params={
        first_name:Fname.value,
        last_name:Lname.value,
        email:Email.value,
        password:Password.value,
        password_confirmation:Cpassword.value,
        phone_no:PhoneNo.value,
    }

    //create customer
    const data= await $fetch('http://165.22.123.187/api/register',
    {
        method:'POST',
        params:params,
        headers:{Accept:'application/vnd.api+json'},
        onResponse({response}){
            if (response.status==200) {
                refresh();
                addCustomer.value=false;
                dialogError.value=null;
                snackbarNote.value='customer created successfully';
                snackbarOpen.value=true;
            }else{
                dialogError.value=response._data.message;
            }
        },
        onResponseError({error}){
            dialogError.value=error.message;
        },
        onRequestError({error}){
            dialogError.value=error.message;
        }
    }
    )
}


const {data, pending, error, refresh, clear }= await useFetch('http://165.22.123.187/api/customers',
        {
            method:'GET',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                myData.value=response._data.data;
                response._data.data.forEach(element => {
                    if (!element.verified) {
                        pendingData.value.push(element);
                    }
                });
            }
        }
    )

onMounted(async ()=>{
    await refresh();
})


async function logMeOut() {
    if (!confirm('confirm logout action')) {
        return
    }
    const data=await $fetch('http://165.22.123.187/api/elogout',
        {
            method:'POST',
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            async onResponse({response}){
                console.log(response);
                if (response.status==200) {
                    localStorage.removeItem('token');
                    window.location.reload();
                    await navigateTo('/');
                }
                
            }

        }
    )
    
}

async function search(){
if (searchQuery.value) {
    const data= await $fetch('http://165.22.123.187/api/customers-search',
        {
            method:'GET',
            params:{search:searchQuery.value},
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                searchData.value=response._data.data;
            }
        }
    )
}
}

onClickOutside(popupItem, () => {
    dialogStatus.value=false;
})



async function deleteCustomer(id) {
    dialogStatus.value=false;
    if (!confirm('confirm this delete action')) {
        return
    }

    const data= await $fetch('http://165.22.123.187/api/customers/'+id,
    {
        method:'DELETE',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            if (response.status==200) {
                refresh();
                snackbarNote.value='customer deleted successfully';
                snackbarSuccess.value=true;
                snackbarOpen.value=true;

            }
        }
    }
    )
}

async function approveCustomer(id,index) {
    dialogStatus.value=false;
    if (!confirm('confirm this approve action')) {
        return
    }

    const data= await $fetch('http://165.22.123.187/api/customers/'+id,
        {
            method:'PATCH',
            params:{verified:'1'},
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if(response.status==200){
                    refresh();
                    snackbarNote.value='Approved successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true;
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
        const data = await $fetch('http://165.22.123.187/api/update-cus-password',
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
                        customerPassword.value=false;
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

async function updateCustomer() {
    dialogStatus.value=false;
    if (updateFname.value && updateLname.value && updatePhoneNo.value) {
        if (updatePhoneNo.value.length<8) {
            dialogError.value='please check your phone number';
            return;
        }
    }else{
        dialogError.value='all fields are required';
        return
    }

    const params={
        first_name:updateFname.value,
        last_name:updateLname.value,
        // email:updateEmail.value,
        phone_no:updatePhoneNo.value,
     }

    const data= await $fetch('http://165.22.123.187/api/customers/'+popItemId.value,
        {
            method:'PATCH',
            params:params,
            headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
            onResponse({response}){
                if(response.status==200){
                    refresh();
                    customerUpdate.value=false;
                    dialogError.value=null;
                    snackbarNote.value='customer update successfully';
                    snackbarSuccess.value=true;
                    snackbarOpen.value=true;
                }
            }
        }
    )
}
</script>