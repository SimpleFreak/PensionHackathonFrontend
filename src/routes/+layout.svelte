<script>
import './app.css'
let {children} = $props()
</script>

<nav>
    <a href="/">Home</a>
    <a href="/register">Registartion</a>
    <a href="/dashboard">dashboard</a>
</nav>

{@render children()}

<style>

</style>