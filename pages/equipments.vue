<template>
    <Popup v-if="false">
        <div v-for="x in 20">Hello kenya Hello kenya Hello kenya Hello kenya Hello kenya</div>
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
            <div v-for="i in 1" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
                <ul class="flex m-auto">
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">Milking Machine</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">5,678</li>
                    <li class="w-52 h-24 text-center py-1 px-2 overflow-y-scroll">Wa njoki Enterprise Wa njoki Enterprise Wa njoki Enterprise Wa njoki Enterprise Wa njoki Enterprise Wa njoki Enterprise Wa njoki EnterpriseWa njoki Enterprise v</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden"><img height="6rem" class="object-contain" src="/assets/images.png"></li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">2024-03-05 21:20:24</li>
                    <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">2024-03-05 21:20:24</li>
                    <li class="w-28 text-center py-1 px-2"><!--Icon name="mdi:dots-vertical"/-->
                    <div class="relative w-0 h-0">
                        <ul v-if="true" class="absolute top-0 left-0 bg-indigo-950 text-white shadow-2xl z-10 p-4">
                            <li class="py-2">update</li>
                            <li class="py-2">delete</li>
                        </ul>
                    </div>
                    </li>
                </ul> 
                 
            </div>
        </div>
        
    </div>
</template>