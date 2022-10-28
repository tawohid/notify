<script lang='ts'>
    import Router from "svelte-spa-router"
    import Login from "./routes/Login.svelte";
    import Dashboard from "./routes/Dashboard.svelte";
    import Notifications from "./routes/Notifications.svelte";
    import NotFound from "./routes/NotFound.svelte";

    let routes = {
        "/": Login,
        "/dashboard/:user": Dashboard,
        "/notifications/:user": Notifications,
        "*": NotFound

    }
</script>


<main>
    <Router {routes} />
</main>


