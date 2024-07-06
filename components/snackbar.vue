<template>
    <div v-if="open"  class="w-full h-0 z-50 relative">
         <div :class="{'bg-green-400':success, 'bg-red-400':!success}" class="absolute py-6 flex top-5 right-10 w-80 opacity-90 rounded-2xl" >
            <div class="flex align-middle w-3/4 pr-3 justify-center">
                {{ message }}
            </div>
            <slot />
         </div>
    </div>
</template>

<script setup>
const close=ref(false);
// const determine=computed(()=>{
//     if (open && close.value) {
        
//         return false;
//     }else{
//         return open;
//     }
// })
defineProps({
    message:String,
    open:{
        type:Boolean,
        default:false
    },
    success:Boolean,
})
</script>