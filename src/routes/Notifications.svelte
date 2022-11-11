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
            read: true,
            visible: true
        },
        {
            id: 124,
            title: "Your email address has been updated",
            description: "You updated your email address on 09/29/2022.\nWe’re providing this notification for your account security, and no additional action is required. \nIf you did not make this change, please visit our Information Protection Center. \n\nThanks for choosing Capital One®.",
            time: "09/29/2022",
            type: "email",
            read: false,
            visible: true
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
            read: false,
            visible: true
        }
    ]

    
    $: active = notifications[0]['id']; 
    $: active_index =  notifications.findIndex(x => x.id == active);
    $: type_filter = "all";
    $: read_filter = "all";
    $: sorted_filter = "newest";
    $: expanded = true;
    $: unread_count = notifications.filter(x => x.read == false).length;

    function returnSorted(notifications, sorted_filter) {
        if (sorted_filter == "newest") {
            return notifications.sort((a, b) => (a.time > b.time) ? -1 : 1)
        } else if (sorted_filter == "oldest") {
            return notifications.sort((a, b) => (a.time > b.time) ? 1 : -1)
        } else {
            return notifications
        }
    }

    $: display = returnSorted(notifications, sorted_filter).filter(x => x.type == type_filter || type_filter == "all").filter(x => x.read == (read_filter == "read") || read_filter == "all").filter(x => x.visible == true)



</script>

<LayoutDashboard count={unread_count}>
        <div class="h-28 w-full bg-sky-900">
            <div class="flex flex-row items-center justify-start h-full">
                <h1 class="text-3xl font-bold ml-16 text-white">Notifications</h1>
            </div>
       </div>
       <div class="flex flex-row bg-white h-full">
            <div class="flex flex-col sr-only  min-w-[33%] {expanded ? 'sm:not-sr-only' : ''}">
                <div class="flex flex-row items-center justify-center -ml-16 h-16 bg-white border-b border-gray-200">
                    <p class="text-lg font-bold ml-16 cursor-pointer text-gray-700" on:click={() => type_filter = "all"} class:font-bold={type_filter == "all"}>All</p>
                    <p class="text-lg font-bold ml-16 cursor-pointer text-gray-700" on:click={() => type_filter = "text"} class:font-bold={type_filter == "text"}>Text</p>
                    <p class="text-lg font-bold ml-16 cursor-pointer text-gray-600" on:click={() => type_filter = "email"} class:font-bold={type_filter == "email"}>Email</p>
                </div>
                

                <div class="flex flex-row items-center justify-center -ml-16 h-16 bg-white border-b border-gray-200">
                    <select class="ml-16 w-40 px-2" name="read" id="read" on:change={(e) => read_filter = e.target.value}>
                        <option value="all">Sort by All</option>
                        <option value="read">Sort by Read</option>
                        <option value="unread">Sort by Unread</option>
                    </select>
                    <select class="ml-16 w-40 px-2" name="sort" id="sort" on:change={(e) => sorted_filter = e.target.value}>
                        <option value="newest">Sort by Newest</option>
                        <option value="oldest">Sort by Oldest</option>
                    </select>
                </div>

                {#if display.length != 0}
                {#each display as notification}
                        {#if notification.id == active}
                            <div class="flex flex-row items-center justify-between p-4 border-b border-gray-200 bg-gray-200 border-l-sky-900 border-l-8">
                                <div class="flex flex-col">
                                    <h1 class="text-md font-bold">{notification.title}</h1>
                                    <div class="flex flex-row items-center">
                                        <p class="text-sm text-gray-500">{notification.time}</p>
                                        {#if notification.read == false}
                                            <div class="ml-2 h-2 w-2 bg-sky-900 rounded-full"></div>
                                        {:else}
                                            <div class="ml-2 h-2 w-2 bg-gray-300 rounded-full" on:click={() => (notification.read = false, unread_count = notifications.filter(x => x.read == false).length)}></div>
                                        {/if}
                                    </div>
                                </div>
                            </div>
                        {/if}
        
                        {#if notification.id != active}
                            <div class="flex flex-row items-center justify-between p-4 border-b border-gray-200 cursor-pointer" on:click={() => (active = notification.id, notification.read = true, unread_count = notifications.filter(x => x.read == false).length )}>
                                <div class="flex flex-col">
                                    <h1 class="text-md font-bold">{notification.title}</h1>
                                    <div class="flex flex-row items-center">
                                        <p class="text-sm text-gray-500">{notification.time}</p>
                                        {#if notification.read == false}
                                            <div class="ml-2 h-2 w-2 bg-sky-900 rounded-full"></div>
                                        {:else}
                                            <div class="ml-2 h-2 w-2 bg-gray-300 rounded-full"></div>
                                        {/if}
                                    </div>
                                </div>
                            </div>
                        {/if}
                {/each}
                {:else}
                <div class="flex flex-row items-center justify-center h-full">
                    <p class="text-lg font-bold text-gray-400">No Notifications</p>
                    </div>
                {/if}
            </div>


            
            <div class="flex flex-col bg-white p-8 mb-4 border-l-gray-200 border-l-2 w-full {expanded ? 'sm:w-2/3' : ''}">
                {#if display.length != 0}
                    <div class="flex flex-row justify-between">
                        <h1 class="text-xl font-bold">{notifications[active_index].title}</h1>
                        <div class="flex flex-row">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-4 cursor-pointer" fill="none" viewBox="0 0 24 24" stroke="gray" on:click={() => expanded = !expanded}>
                                <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 3.75v4.5m0-4.5h4.5m-4.5 0L9 9M3.75 20.25v-4.5m0 4.5h4.5m-4.5 0L9 15M20.25 3.75h-4.5m4.5 0v4.5m0-4.5L15 9m5.25 11.25h-4.5m4.5 0v-4.5m0 4.5L15 15" />
                            </svg>
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-4 cursor-pointer" fill="none" viewBox="0 0 24 24" stroke="gray" on:click={() => window.print()}>
                                <path stroke-linecap="round" stroke-linejoin="round" d="M6.72 13.829c-.24.03-.48.062-.72.096m.72-.096a42.415 42.415 0 0110.56 0m-10.56 0L6.34 18m10.94-4.171c.24.03.48.062.72.096m-.72-.096L17.66 18m0 0l.229 2.523a1.125 1.125 0 01-1.12 1.227H7.231c-.662 0-1.18-.568-1.12-1.227L6.34 18m11.318 0h1.091A2.25 2.25 0 0021 15.75V9.456c0-1.081-.768-2.015-1.837-2.175a48.055 48.055 0 00-1.913-.247M6.34 18H5.25A2.25 2.25 0 013 15.75V9.456c0-1.081.768-2.015 1.837-2.175a48.041 48.041 0 011.913-.247m10.5 0a48.536 48.536 0 00-10.5 0m10.5 0V3.375c0-.621-.504-1.125-1.125-1.125h-8.25c-.621 0-1.125.504-1.125 1.125v3.659M18 10.5h.008v.008H18V10.5zm-3 0h.008v.008H15V10.5z" />                              
                            </svg>
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-4 cursor-pointer" fill="none" viewBox="0 0 24 24" stroke="gray" on:click={() => (notifications[active_index].visible = false)}>
                                <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />                              
                            </svg>
                        </div>
                    </div>
                    <div class="flex flex-col mt-8">
                        <p class="text-gray-500 whitespace-pre-line">{notifications[active_index].description}</p>
                    </div>
                    <div class="flex flex-col items-end justify-end mt-auto">
                        <!-- navigation arrow keys -->
                        <div class={expanded ? 'hidden' : 'flex flex-row mt-8'}>
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7 mr-4 cursor-pointer" fill="none" viewBox="0 0 24 24" stroke="gray" on:click={() => ((active_index != 0) ? active_index-- : active_index = notifications.length - 1)}>
                                <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
                            </svg>
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7 mr-4 cursor-pointer" fill="none" viewBox="0 0 24 24" stroke="gray" on:click={() => ((active_index != notifications.length - 1) ? active_index++ : active_index = 0)}>
                                <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
                            </svg>
                        </div>
                       
                    </div>
                {:else}
                    <div class="flex flex-col">
                        <h1 class="text-xl font-bold">No Notifications Selected</h1>
                    </div>
                {/if}

        </div>
</LayoutDashboard>