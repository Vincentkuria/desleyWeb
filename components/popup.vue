<template>
    <div>
        <div class="w-full h-0 relative">
            <div class="z-50 flex justify-items-center h-screen w-full bg-gray-700 bg-opacity-65 absolute">
                <div class="m-auto p-4 w-fit h-fit max-w-screen-sm  max-h-screen overflow-scroll  bg-white">
                    <slot/>
                </div>
            </div>
        </div>
    </div>
</template>