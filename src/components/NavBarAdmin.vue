<template>
    <nav class="navbar">
        <div class="logo">
            <h1>FitRoutine</h1>
        </div>
        <ul class="nav-links">
            
        </ul>
    </nav>

</template>

<style scoped>
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 30px;
    background-color: #303030;
    width: 96.1%;
    z-index: 1000;
    position: fixed;
}

.navbar .logo h1 {
    color: #fff;
}

.navbar .nav-links {
    list-style: none;
    display: flex;
    gap: 20px;
    position: relative;
}

.navbar .nav-links li {
    position: relative;
}

.navbar .nav-links li a {
    color: #fff;
    text-decoration: none;
    font-size: 16px;
}

.dropdown-menu {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    background-color: #333;
    list-style: none;
    padding: 0;
    margin: 0;
    border-radius: 4px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    z-index: 1;
}

.dropdown-menu li {
    padding: 10px 20px;
}

.dropdown-menu li a {
    color: #fff;
    text-decoration: none;
    display: block;
}

.dropdown-menu li a:hover {
    background-color: #555;
}

.dropdown:hover .dropdown-menu {
    display: block;
}
</style>