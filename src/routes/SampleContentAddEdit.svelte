<script>
	let sampleData = [
		{
			name:"Toyota",
			desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  ",
			
		},
		{
			name:"Maruti",
			desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  ",
			
		},
		{
			name:"Mercedez",
			desc:"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown  ",
			
		}
	];

	let sampleItems = [...sampleData];

	
	
		
	function filterContent(e) {
		let search = e.target.value;
		console.log('e.target.value',e.target.value)
		sampleItems = [...sampleData]?.filter(item=> search ? item?.name?.toLowerCase().includes(search.toLowerCase()) : true);
		console.log('sampleItems',sampleItems)
		
  	}

	//add company and modal
	let addContentPopup = false;
	
	let name = ''
	let desc = ''

	function addCompany(){
		
		sampleData.unshift({name:name,desc:desc})
		sampleItems.unshift({name:name,desc:desc})
		sampleData =  sampleData;
		sampleItems = sampleItems;
		name = '';
		desc = '';
		addContentPopup = false;
		

	}

	
	
</script>


<!-- drawer init and show -->
	<div class="text-right">
	<button class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800" type="button" data-drawer-target="drawer-form" data-drawer-show="drawer-form" aria-controls="drawer-form" on:click={() => (addContentPopup = true)}>
	Add Content
	</button>
</div>

<div class="relative">
	<div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
		<svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
	</div>
	<input type="search" id="search" 
	class="block w-full p-4 pl-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search" 
	 on:keyup={filterContent} />

</div>
<br/>


<div class="modal-wrapper flex flex-wrap justify-between">
{#each sampleItems as item}
	<button class="card-block modal-block block max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700  " >
		<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{item.name}</h5>
		<p class="font-normal text-gray-700 dark:text-gray-400">{item.desc}</p>
	</button>

{/each}

</div>
{#if sampleItems.length == 0}
<p class="font-bold text-center">No data found</p>
{/if}
 
 
 




  
  <!-- Company modal -->
  <div id="defaultModal" tabindex="-1" aria-hidden="true" class="fixed top-0 left-0 right-0 z-50  w-full p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-[calc(100%-1rem)] max-h-full align-center justify-center	items-center	 {addContentPopup?'flex':'hidden'}">
	  <div class="relative w-full max-w-2xl max-h-full">
		  <!-- Modal content -->
		  <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
			  <!-- Modal header -->
			  <div class="flex items-start justify-between p-4 border-b rounded-t dark:border-gray-600">
				  <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
					  Add Content
				  </h3>
				  <button type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white" data-modal-hide="defaultModal" on:click={() => {
					addContentPopup = false;
					
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

