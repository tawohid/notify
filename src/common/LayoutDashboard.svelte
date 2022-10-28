<div class="bg-gray-100 flex flex-col h-screen justify-between items-center">
  <div class="bg-white w-full h-16 shadow-sm">
    <div class="container mx-auto max-w-screen-lg  h-full flex items-center">
      <div class="flex-1">
        <a href="/#/dashboard/1/">
          <img src="https://ecm.capitalone.com/CI_Common/assets/images/logos/capital-one-logo.svg" alt="Logo" class="h-10 m-4">
        </a>
      </div>
      <div class="flex-1">
        <div class="flex justify-end ">
          
          <a href="/#/notifications/1/">
            <button class="relative p-1 mr-6 -mt-1 rounded-full hover:bg-gray-200">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="w-6 h-6"
              >
                <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9" />
                <path d="M13.73 21a2 2 0 0 1-3.46 0" />
              </svg>
              <span class="badge">
                5
              </span>
            </button>
          </a>

          <div class="relative">
            <button  id="dropdownAvatarNameButton" data-dropdown-toggle="dropdownAvatarName" class="flex items-center text-sm font-medium text-gray-900 rounded-full hover:text-primary-50 md:mr-0" type="button">
              <span class="sr-only">Open user menu</span>
              Khalid Hossain
              <svg class="w-4 h-4 mx-1.5" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
          </button>
          
          <!-- Dropdown menu -->
          <div id="dropdownAvatarName" class="hidden z-10 w-44 bg-white  divide-y divide-gray-100 shadow">
              <div class="py-3 px-4 text-sm text-gray-900">
                <div class="truncate">khalid@voscra.com</div>
              </div>
              <div class="py-1">
                <a href="/#" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Sign out</a>
              </div>
          </div>
            
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="w-full h-4/5">
    <slot></slot>
  </div>
    
  
    <div class="bg-gray-200 w-full h-18 shadow-sm mt-auto">
      <div class="container mx-auto max-w-screen-lg px-6 py-3">
        <div class="flex justify-between items-center">
          <div class="text-sm text-gray-600 font-light">
            © 2022 Capital One
          </div>
          <div class="text-sm text-gray-600 font-light">
            CS4485 Project
          </div>
        </div>
      </div>
    </div>

</div>





<style>
  /* unread message count */
  .badge {
    display: inline-block;
    position: absolute;
    top: 0;
    background-color: #dd1a09;
    color: #d7e6fd;
    right: 0;
    border-radius: 9999px;
    font-size: 12px;
    min-width: 18px;
    line-height: 18px;
    min-height: 18px;
    text-align: center;
  }


</style>