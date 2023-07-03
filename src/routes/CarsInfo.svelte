<script>
	import { spring } from 'svelte/motion';

	let count = 10;
	let showDrawer = false;
	let selctedCompany  = null;
	let selectedModels  = null;
	
	let carCompainesData = [
		{
			name:"Toyota",
			desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  ",
			models:[{
				name:"Toyota Model 1",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},
			{
				name:"Toyota Model 2",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},
			{
				name:"Toyota Model 3",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},{
				name:"Toyota Model 4",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			}]
		},
		{
			name:"Maruti",
			desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  ",
			models:[{
				name:"Maruti Model 1",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},
			{
				name:"Maruti Model 2",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},
			{
				name:"Maruti Model 3",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},{
				name:"Maruti Model 4",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			}]
		},
		{
			name:"Mercedez",
			desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  ",
			models:[{
				name:"Mercedez Model 1",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},
			{
				name:"Mercedez Model 2",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},
			{
				name:"Mercedez Model 3",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			},{
				name:"Mercedez Model 4",
				desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  "
			}]
		}
	];

	let carCompaines = [...carCompainesData];

	
	
		
	function filterContent(e) {
		let search = e.target.value;
		
		carCompaines = [...carCompainesData]?.filter(item=> search ? item?.name?.toLowerCase().includes(search.toLowerCase()) : true);
  	}

	//add company and modal
	let addCompanyPopup = false;
	let addModalPopup = false;
	let name = ''
	let desc = ''

	function addCompany(){
		if(addCompanyPopup){
			carCompainesData.unshift({name:name,desc:desc,models:[]})
			carCompaines.unshift({name:name,desc:desc,models:[]})
			carCompainesData =  carCompainesData;
			carCompaines = carCompaines;
		}
		else{
			try{
			let models = [...selctedCompany.models];
			models.unshift({name:name,desc:desc})
			//index of selected company 
			let index = carCompainesData.findIndex(item=> item.name === selctedCompany.name);
			carCompainesData[index].models.unshift({name:name,desc:desc})
			carCompainesData =  carCompainesData;
			carCompaines = carCompainesData;
			selectedModels = models;
			console.log('models',selectedModels)
			
		}
		catch(err){
			console.log(err);
		}
			
		}
		
		
		
		name = '';
		desc = '';
		addCompanyPopup = false;
		addModalPopup = false

	}

	
	
</script>


<!-- drawer init and show -->
	<div class="text-right">
	<button class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800" type="button" data-drawer-target="drawer-form" data-drawer-show="drawer-form" aria-controls="drawer-form" on:click={() => (showDrawer = !showDrawer)}>
	Show Compaines
	</button>
</div>

{#if selctedCompany == null}
<h3 class="font-bold text-center ">Please select a company from sidebar.</h3>
{/if}

{#if selctedCompany != null}
<h1 class="text-3xl font-medium">{selctedCompany.name}</h1>

<p>{selctedCompany.desc}</p>
<br/>
<div class="flex justify-between">
<h2 class="text-2xl font-medium">Related Models</h2>
<button class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800" type="button" data-drawer-target="drawer-form" data-drawer-show="drawer-form" aria-controls="drawer-form" on:click={() => (addModalPopup = true)}>
	Add Modal
	</button>
</div>
<div class="modal-wrapper flex flex-wrap justify-between">
{#each selectedModels as modal}
	<button class="card-block modal-block block max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700  " >
		<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{modal.name}</h5>
		<p class="font-normal text-gray-700 dark:text-gray-400">{modal.desc}</p>
	</button>

{/each}
</div>
{/if}
 
 <!-- drawer component -->
 <div id="drawer-form" class="fixed top-0 left-0 z-40 h-screen p-4 overflow-y-auto transition-transform  bg-white w-80 dark:bg-gray-800 {showDrawer?'':'-translate-x-full'}" tabindex="-1" aria-labelledby="drawer-form-label">
	<button type="button" data-drawer-hide="drawer-form" aria-controls="drawer-form" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 absolute top-2.5 right-2.5 inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white" on:click={() => (showDrawer = !showDrawer)} >
	   <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
	   <span class="sr-only">Close menu</span>

	</button>
		<div class="text-right">
			<button class="text-white btn-block bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800" type="button" data-drawer-target="drawer-form" data-drawer-show="drawer-form" aria-controls="drawer-form" on:click={() => (addCompanyPopup = true)}>
			Add  Company
			</button>
		</div>
		<br/>
		<div class="relative">
			<div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
				<svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
			</div>
			<input type="search" id="search" 
			class="block w-full p-4 pl-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search" 
			 on:keyup={filterContent} />

		</div>
	<br/>
	 
{#each carCompaines as company}
	<button class="card-block block max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700 {selctedCompany?.name == company.name ?'selected':''} " 
	on:click={() => {
		selctedCompany = company;
		selectedModels = company.models;
	}}
	>
		<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{company.name}</h5>
		<p class="font-normal text-gray-700 dark:text-gray-400">{company.desc}</p>
	</button>

{/each}

{#if carCompaines.length == 0}
<p class="font-bold text-center text-white">No data found</p>
{/if}



 </div>
 




  
  <!-- Company modal -->
  <div id="defaultModal" tabindex="-1" aria-hidden="true" class="fixed top-0 left-0 right-0 z-50  w-full p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-[calc(100%-1rem)] max-h-full align-center justify-center	items-center	 {addCompanyPopup || addModalPopup?'flex':'hidden'}">
	  <div class="relative w-full max-w-2xl max-h-full">
		  <!-- Modal content -->
		  <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
			  <!-- Modal header -->
			  <div class="flex items-start justify-between p-4 border-b rounded-t dark:border-gray-600">
				  <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
					  {addCompanyPopup?"Add Company":"Add Modal"}
				  </h3>
				  <button type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white" data-modal-hide="defaultModal" on:click={() => {
					addCompanyPopup = false;
					addModalPopup = false;
					}}>
					  <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
					  <span class="sr-only">Close modal</span>
				  </button>
			  </div>
			  <!-- Modal body -->
			  <div class="p-6 space-y-6">
				  
<form on:submit={addCompany}>
    <div class="grid gap-4 mb-12 md:grid-cols-1">
        <div>
            <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Name</label>
            <input type="text" bind:value={name} id="name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Name" required>
        </div>
        <div>
            <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Description</label>
			<textarea id="message" bind:value={desc} rows="4" class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Write  here..." required></textarea>

        </div>  
        
    </div>
    
   
    <button type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Submit</button>
</form>

			  </div>
			  
		  </div>
	  </div>
  </div>
  

<style>
#drawer-form	{
	padding-top: 50px;
}

.card-block {
    width: 100%;
    margin-bottom: 20px;
	text-align: left;
}
.card-block.selected{
	border-color: rgb(34, 118, 170);
}
.modal-block{
	max-width: 48%;
}


</style>

