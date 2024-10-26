<script>
    import '../app.css'
    let {children} = $props()
    </script>
    
    <nav>
        <a href="/dashboard/add_pers">Add Person</a>
        <a href="/dashboard">dashboard</a>
    </nav>
    
    {@render children()}
    
    <style>
    
    </style>