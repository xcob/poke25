<template>

<nav class="navbar">
    <ul>
      <li>
        <NuxtLink to="/card" class="nav-link">
          Card page
        </NuxtLink>
        </li>
        <li>
        <NuxtLink to="/dex" class="nav-link">
          Dex page
        </NuxtLink>
      </li>
    </ul>
  </nav>
  <div>
  
  </div>  
</template>

<style scoped>
.navbar {
  background-color: #333;
  padding: 1rem 0;
  width: 100%;
  margin: 0px;
}

.navbar ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
}

.nav-link {
  color: #fff;
  padding: 0.5rem 1rem;
  text-decoration: none;
}

.nav-link:hover {
  background-color: #555;
}
</style>