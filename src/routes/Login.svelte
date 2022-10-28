<script>
  import LayoutLogin from "../common/LayoutLogin.svelte";
</script>

<LayoutLogin>
  <div class="bg-white rounded py-20 px-20 m-16 flex flex-col items-center justify-center">
    <img class="rounded-full h-16 w-16" src="https://ssl.gstatic.com/accounts/ui/avatar_2x.png" alt="user avatar" />
    <h1 class="text-2xl mt-4">Sign In</h1>
    <div class="mt-8 mb-4">
      <div class="mb-4">
        <input class="border-solid border border-gray-400 hover:border-primary-50 focus:border-primary-50 px-6 py-3" placeholder="Username" required />
      </div>
      <div>
        <input class="border-solid border border-gray-400  hover:border-primary-50 px-6 py-3" type="password" placeholder="Password" required />
      </div>
      <div class="my-4 flex items-center">
        <input class="h-4 w-4 mr-2" type="checkbox"/>
        <label for="remember">Remember me</label>
      </div>
      <a href='/#/dashboard/1'> 
        <button class="bg-primary-50 hover:bg-primary-100 text-white font-bold w-full py-3">
        Sign In 
        </button>
      </a>
    </div>
    <a href="/#/" class="self-start">Forgot the password?</a>
  </div>
</LayoutLogin>