<template>
<div>
    <div class="flex bg-indigo-950 text-white justify-between my-3 py-3 mx-10 px-10 print:hidden" id="orderReports">
        <h1 class="text-lg">Order Reports</h1>
        <div class="flex flex-row">
            <h1 class="bg-indigo-800 py-2 px-4 mx-2 hover:cursor-pointer " @click="getOrderReports(); showing=1">Generate report</h1>
            <h1 class="bg-indigo-800 py-2 px-2 hover:cursor-pointer" v-if="myData!=null && showing==1" @click="printReport">Print report</h1>
        </div>
        
    </div>
    <div v-if="myData!=null && showing==1">
        <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
            <ul class="flex m-auto">
                <li class="w-48 text-center p-2">Customer name</li>
                <li class="w-48 text-center p-2">Email</li>
                <li class="w-48 text-center p-2">Payment</li>
                <li class="w-28 text-center p-2">Item</li>
                <li class="w-28 text-center p-2">Count</li>
                <li class="w-28 text-center p-2">Date Time</li>
            </ul>
        </div>
        <div v-for="(item,index) in myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
            <ul class="flex m-auto">
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.customer.first_name+" "+item.customer.last_name }}</li>
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.customer.email}}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.payment.amount}}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.equipment!=null ? item.equipment.name :  item.spare.name!==null? item.spare.name : ' ' }}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.count}}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                
            </ul> 
             
        </div>

    </div>

    <!--  -->
    <div class="flex bg-indigo-950 text-white justify-between my-3 py-3 mx-10 px-10 print:hidden" id="serviceReports">
        <h1 class="text-lg">Service Reports</h1>
        <div class="flex flex-row">
            <h1 class="bg-indigo-800 py-2 px-4 mx-2 hover:cursor-pointer" @click="getServiceReports(); showing=2">Generate report</h1>
            <h1 class="bg-indigo-800 py-2 px-2 hover:cursor-pointer" @click="printReport" v-if="myData!=null && showing==2">Print report</h1>
        </div>
        
    </div>
    <div v-if="myData!=null && showing==2">
        <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
            <ul class="flex m-auto">
                <li class="w-48 text-center p-2">Customer name</li>
                <li class="w-48 text-center p-2">Email</li>
                <li class="w-48 text-center p-2">Payment</li>
                <li class="w-28 text-center p-2">Item</li>
                <li class="w-28 text-center p-2">Count</li>
                <li class="w-28 text-center p-2">Date Time</li>
            </ul>
        </div>
        <div v-for="(item,index) in myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
            <ul class="flex m-auto">
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.customer.first_name+" "+item.customer.last_name }}</li>
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.customer.email}}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.payment.amount}}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.service.name!=null ? item.service.name : " "}}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.count}}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                
            </ul> 
             
        </div>
    </div>

    <!--  -->
    <div class="flex bg-indigo-950 text-white justify-between my-3 py-3 mx-10 px-10 print:hidden" id="financialReports">
        <h1 class="text-lg">Financial Reports</h1>
        <div class="flex flex-row">
            <h1 class="bg-indigo-800 py-2 px-4 mx-2 hover:cursor-pointer" @click="getFinancialReports(); showing=3">Generate report</h1>
            <h1 class="bg-indigo-800 py-2 px-2 hover:cursor-pointer" @click="printReport" v-if="myData!=null && showing==3">Print report</h1>
        </div>
        
    </div>
    <div v-if="myData!=null && showing==3">
        <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
            <ul class="flex m-auto">
                <li class="w-48 text-center p-2">Payment Code</li>
                <li class="w-48 text-center p-2">Amount</li>
                <li class="w-48 text-center p-2">Transaction</li>
                <li class="w-28 text-center p-2">Status</li>
                <li class="w-28 text-center p-2">Date Time</li>
            </ul>
        </div>
        <div v-for="(item,index) in myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
            <ul class="flex m-auto">
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.payment_code }}</li>
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.amount}}</li>
                <li class="w-28 text-left py-1 px-2 overflow-hidden text-ellipsis">{{ item.customer!=null ? "Revenue \n Customer: "+item.customer.first_name+" "+item.customer.last_name: "Expense \n Supplier: "+item.supplier.company_name}}</li>
                <li :class="{'text-red-600':item.status.finance=='pending','text-green-600':item.status.finance=='approved'}" class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.status.finance }}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.created_at}}</li>
                
            </ul> 
             
        </div>
    </div>

    <!--  -->

    <div class="flex bg-indigo-950 text-white justify-between my-3 py-3 mx-10 px-10 print:hidden" id="supplierReports">
        <h1 class="text-lg">Supplier Reports</h1>
        <div class="flex flex-row">
            <h1 class="bg-indigo-800 py-2 px-4 mx-2 hover:cursor-pointer" @click="getSupplierReports(); showing=4">Generate report</h1>
            <h1 class="bg-indigo-800 py-2 px-2 hover:cursor-pointer" @click="printReport" v-if="myData!=null && showing==4">Print report</h1>
        </div>
        
    </div>
    <div v-if="myData!=null && showing==4">
        <div class="w-full bg-indigo-950 text-white h-2/3 flex  justify-items-center ">
            <ul class="flex m-auto">
                <li class="w-48 text-center p-2">Supplier</li>
                <li class="w-48 text-center p-2">Inventory</li>
                <li class="w-28 text-center p-2">Count</li>
                <li class="w-28 text-center p-2">Amount</li>
                <li class="w-28 text-center p-2">Status</li>
                <li class="w-28 text-center p-2">Date Time</li>
            </ul>
        </div>
        <div v-for="(item,index) in myData" class="w-full p-3 flex  justify-items-center shadow-lg m-2 ">
            <ul class="flex m-auto">
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{item.supplier.company_name}}</li>
                <li class="w-48 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.inventory.name }}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.count }}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.count*item.inventory.price }}</li>
                <li :class="{'text-red-600':item.status.manager=='pending','text-green-600':item.status.manager=='approved'}" class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.status.manager }}</li>
                <li class="w-28 text-center py-1 px-2 overflow-hidden text-ellipsis">{{ item.created_at }}</li>
                
            </ul> 
             
        </div>
    </div>
</div>

</template>

<script setup >

const myData=ref(null);
const showing=ref(null);

 const printReport = () => {
    window.print();
 }


async function getOrderReports() {
    const data = await $fetch('http://127.0.0.1:8000/api/all-order-reports',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            myData.value=null;
            myData.value=response._data.data;
            // this.$refs.orderReports.scrollIntoView({behavior: "smooth"});
            document.getElementById("orderReports").offsetTop;
        },
        onRequestError({error}){
            
            console.log(error);
        },
        onResponseError({request,response,options}){
            
            console.log(response);
        }
    }
)
}

async function getServiceReports() {
    const data = await $fetch('http://127.0.0.1:8000/api/all-service-reports',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            myData.value=null;
            myData.value=response._data.data;
            // this.$refs.serviceReports.scrollIntoView({behavior: "smooth"});
            document.getElementById("serviceReports").offsetTop;
        },
        onRequestError({error}){
            
            console.log(error);
        },
        onResponseError({request,response,options}){
            
            console.log(response);
        }
    }
)
}

async function getFinancialReports() {
    const data = await $fetch('http://127.0.0.1:8000/api/all-finance-reports',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            myData.value=null;
            myData.value=response._data.data;
            // this.$refs.serviceReports.scrollIntoView({behavior: "smooth"});
            document.getElementById("financialReports").offsetTop;
        },
        onRequestError({error}){
            
            console.log(error);
        },
        onResponseError({request,response,options}){
            
            console.log(response);
        }
    }
)
}

async function getSupplierReports() {
    const data = await $fetch('http://127.0.0.1:8000/api/all-supplier-resource',
    {
        method:'GET',
        headers:{Accept:'application/vnd.api+json',Authorization:'Bearer '+localStorage.getItem('token')},
        onResponse({response}){
            myData.value=null;
            myData.value=response._data.data;
            // this.$refs.serviceReports.scrollIntoView({behavior: "smooth"});
            document.getElementById("supplierReports").offsetTop;
        },
        onRequestError({error}){
            
            console.log(error);
        },
        onResponseError({request,response,options}){
            
            console.log(response);
        }
    }
)
}
</script>