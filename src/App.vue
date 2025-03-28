<template>
  <div class="layout">
    <!-- Sidebar Navigation -->
    <aside class="sidebar">
      <nav>
        <router-link to="/">
          <span class="icon">🏡</span> Home
        </router-link>
        <router-link to="/add">
          <span class="icon">🆕</span> Add Contact
        </router-link>
        <router-link to="/contacts">
          <span class="icon">📇</span> Contact List
        </router-link>
      </nav>
    </aside>

    <!-- Main Content -->
    <main class="content">
      <router-view /> <!-- This renders the page based on the route -->
    </main>
  </div>
</template>

<style>
*
{
  margin:0px;
  padding:0px;
}

.layout {
  display: flex;
  height: 100vh;
}


.sidebar {
  width: 250px;
  background: #34495e;
  color: white;
  padding: 20px;
  display: flex;
  flex-direction: column;
}


nav {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

nav a {
  color: white;
  text-decoration: none;
  font-size: 18px;
  padding: 12px;
  border-radius: 5px;
  display: flex;
  align-items: center;
  gap: 10px;
  transition: 0.3s;
}

nav a:hover {
  background: #1abc9c;
}


.icon {
  font-size: 20px;
}


.content {
  flex: 1;
  padding: 20px;
}
</style>
