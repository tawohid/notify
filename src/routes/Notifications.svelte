<script>
    import LayoutDashboard from "../common/LayoutDashboard.svelte";

    let notifications = [
        {
            id: 123,
            title: "You're projected to owe a balance when your loan matures on 11/31/2022",
            description: "Khalid,\n\
            Due to events that occurred during the life of your loan, you're projected to have\n\n\
            a balance due when your loan matures on 11/31/2022. You can choose to lower the balance due at the end of your loan now by making an additional one-time payment, or adding a little extra to your current monthly payments.‌\n\n\
            Not sure how this happened? Activate your account in a few easy steps to check out our Auto Loan Tracker and see more details.",
            time: "10/11/2022",
            type: "text",
        },
        {
            id: 124,
            title: "Your email address has been updated",
            description: "You updated your email address on 09/29/2022.\nWe’re providing this notification for your account security, and no additional action is required. \nIf you did not make this change, please visit our Information Protection Center. \n\nThanks for choosing Capital One®.",
            time: "09/29/2022",
            type: "email",
        },
        {
            id: 321,
            title: "You're projected to owe a balance when your loan matures on 08/31/2022",
            description: "Khalid,\n\
            Due to events that occurred during the life of your loan, you're projected to have\n\n\
            a balance due when your loan matures on 08/31/2022. You can choose to lower the balance due at the end of your loan now by making an additional one-time payment, or adding a little extra to your current monthly payments.‌\n\n\
            Not sure how this happened? Activate your account in a few easy steps to check out our Auto Loan Tracker and see more details.",
            time: "08/11/2022",
            type: "text",
        },
    ]

    
    $: active = notifications[0]['id'];
    $: active_index =  notifications.findIndex(x => x.id == active);
    $: sorted = notifications;
    $: sorted_togle = false;
    $: filter = "all";


</script>

<LayoutDashboard>
        <div class="h-28 w-full bg-sky-900">
            <div class="flex flex-row items-center justify-start h-full">
                <h1 class="text-3xl font-bold ml-16 text-white">Notifications</h1>
            </div>
       </div>
       <div class="flex flex-row bg-white h-full">
            <div class="flex flex-col sr-only sm:not-sr-only min-w-[33%]">
                <div class="flex flex-row items-center justify-center -ml-16 h-16 bg-white border-b border-gray-200">
                    <p class="text-lg font-bold ml-16 cursor-pointer text-gray-700" on:click={() => filter = "all"} class:font-bold={filter == "all"}>All</p>
                    <p class="text-lg font-bold ml-16 cursor-pointer text-gray-700" on:click={() => filter = "text"} class:font-bold={filter == "text"}>Text</p>
                    <p class="text-lg font-bold ml-16 cursor-pointer text-gray-600" on:click={() => filter = "email"} class:font-bold={filter == "email"}>Email</p>
                </div>
               
                <div class="flex flex-row items-center justify-center -ml-16 h-16 bg-white border-b border-gray-200">
                    {#if sorted_togle}
                    <p class="text-lg font-bold ml-16 text-gray-400">Sorted by Oldest</p>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 ml-2" fill="none" viewBox="0 0 24 24" stroke="gray" on:click={() => (sorted_togle = false,sorted = notifications.sort((a, b) => (a.time < b.time) ? 1 : -1))}>
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 15l7-7 7 7" />
                    </svg>
                    {:else}
                    <p class="text-lg font-bold ml-16 text-gray-400">Sorted by Newest</p>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 ml-2" fill="none" viewBox="0 0 24 24" stroke="gray" on:click={() => (sorted_togle = true,sorted = notifications.sort((a, b) => (a.time > b.time) ? 1 : -1))}>
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                    </svg>
                    {/if}
                </div>
                {#each sorted as notification}
                    {#if filter == "all" || filter == notification.type}
                        {#if notification.id == active}
                            <div class="flex flex-row items-center justify-between p-4 border-b border-gray-200 bg-gray-200 border-l-sky-900 border-l-8">
                                <div class="flex flex-col">
                                    <h1 class="text-md font-bold">{notification.title}</h1>
                                    <p class="text-sm text-gray-500">{notification.time}</p>
                                </div>
                                
                            </div>
                        {/if}
        
                        {#if notification.id != active}
                            <div class="flex flex-row items-center justify-between p-4 border-b border-gray-200 cursor-pointer" on:click={() => active = notification.id}>
                                <div class="flex flex-col">
                                    <h1 class="text-md font-bold">{notification.title}</h1>
                                    <p class="text-sm text-gray-500">{notification.time}</p>
                                </div>
                            </div>
                        {/if}
                    {/if}
                {/each}
            </div>


            <div class="flex flex-col bg-white p-8 mb-4 border-l-gray-200 border-l-2 w-full sm:w-2/3">
                <div class="flex flex-col">
                    <h1 class="text-xl font-bold">{notifications[active_index].title}</h1>
                </div>
                <div class="flex flex-col mt-8">
                    <p class="text-gray-500 whitespace-pre-line">{notifications[active_index].description}</p>
                </div>
                <div class="flex flex-col items-end justify-end mt-auto">
                    <p class="text-sm text-gray-500">{notifications[active_index].time}</p>
            </div>

        </div>
</LayoutDashboard>