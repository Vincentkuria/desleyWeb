<template>
    <Popup v-if="customerUpdate || customerPassword ">
        <div v-if="customerUpdate">
            <form>
                <div class="py-4">
                    <label class="block pb-2" for="fn">First Name</label>
                    <input class="border-2 border-gray-600 rounded-md" id="fn" type="text">
                </div>
                <div class="py-4">
                    <label class="block pb-2" for="ln">Last Name</label>
                    <input class="border-2 border-gray-600 rounded-md" id="ln" type="text">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="e">Email</label>
                    <input  class="border-2 border-gray-600 rounded-md" id="e" type="email">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="pn">Phone No</label>
                    <input  class="border-2 border-gray-600 rounded-md" id="pn" type="number">
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white py-2 px-6 rounded-full" @click="updateCustomer">Update</button>
                    <button @click="customerUpdate=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
                
            </form>
        </div>
        <div v-if="customerPassword">
            <form>
                <div class="py-4">
                    <label class="block pb-2" for="pas">Password</label>
                    <input class="border-2 border-gray-600 rounded-md" id="pas" type="password">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="new_pas">New password</label>
                    <input  class="border-2 border-gray-600 rounded-md" id="new_pas" type="password">
                </div>
                <div class="py-4">
                    <label  class="block pb-2" for="con_pas">Confirm password</label>
                    <input  class="border-2 border-gray-600 rounded-md" id="con_pas" type="password">
                </div>
                <div class="flex justify-between w-72">
                    <button class=" bg-indigo-950 text-white p-2 rounded-full">Change password</button>
                    <button @click="customerPassword=false" class="bg-indigo-950 text-white py-2 px-3 rounded-full">Cancel</button>
                </div>
                
            </form>
        </div>
    </Popup>
    <div class="h-screen">
        <div class="h-1/5">

            <div class="h-1/3 w-full flex shadow-2xl">
                <div class="w-full h-full flex pb-1 ms-7">
                    
                    <input class="w-1/2 border-2 px-2 rounded-lg border-indigo-950" type="text" placeholder="Search" >
                    <button class="bg-indigo-950 text-white mx-2 p-2 px-4 rounded-full">
                        
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
                        </svg>

                    </button>
                </div>

                <button class=" text-white  bg-indigo-950 rounded-md flex text-center px-4 py-2 mb-2 mr-6">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
                    </svg>
                    Add 
                </button>

                <div class="w-40 flex h-5/6 mr-4 border-indigo-950 border-2">
                    <button class="w-1/2 text-white bg-indigo-950 h-full flex justify-center align-middle">
                        All
                    </button>
                    <button class="w-1/2 h-full align-middle flex justify-center">
                        Pending
                    </button>
                </div>
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
            <div v-for="i in 1" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">Vincent kuria</li>
                    <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">vinvincent254@gmail.com11111111111111</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">0712051540</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis text-red-600">pending</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">2024-03-05 21:20:24</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">2024-03-05 21:20:24</li>
                    <li class="w-28 text-center py-1 px-2">
                        <svg @click="dialogStatus=true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z" />
                        </svg>

                    <div class="relative w-0 h-0">
                        
                            <ul v-if="dialogStatus" ref="popupItem" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                                <li class="py-2 hover:cursor-pointer" @click="approveCustomer">approve</li>
                                <li class="py-2 hover:cursor-pointer" @click="customerUpdate=true">update</li>
                                <li class="py-2 hover:cursor-pointer" @click="customerPassword=true">change password</li>
                                <li class="py-2 hover:cursor-pointer" @click="deleteCustomer">delete</li>
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
const popupItem=ref(null);

onClickOutside(popupItem, () => {
    dialogStatus.value=false;
})



function deleteCustomer() {
    dialogStatus.value=false;
    if (confirm('confirm this delete action')) {
        
    }
}

function approveCustomer() {
    dialogStatus.value=false;
    if (confirm('confirm this approve action')) {
        
    }
}

function updateCustomer() {
    dialogStatus.value=false;
    
}
</script>