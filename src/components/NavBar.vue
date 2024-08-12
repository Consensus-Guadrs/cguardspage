<template>
  <nav class="navbar">
    <div class="logo">
      <a href="/"><img src="/logo.png" alt="Logo"></a>
      <p>Blockchain's power for big goals</p>
    </div>
    <div class="links">
      <a :href="contactLinks.github" target="_blank">
        <img :src="githubIcon" alt="GitHub">
      </a>
      <a :href="contactLinks.gmail" target="_blank">
        <img :src="emailIcon" alt="Email">
      </a>
    </div>
    <ul :class="['nav-links', { 'nav-active': isNavActive }]">
      <li><router-link to="/" @click="closeNav">Home</router-link></li>
      <li><router-link to="/validate" @click="closeNav">Validate</router-link></li>
      <li><router-link to="/mainnets" @click="closeNav">Mainnets</router-link></li>
      <li><router-link to="/testnets" @click="closeNav">Testnets</router-link></li>
      <li><router-link to="/community-contributions" @click="closeNav">Community</router-link></li>
      <li><router-link to="/technical-contributions" @click="closeNav">Technical</router-link></li>
    </ul>
    <div class="burger" @click="toggleNav">
      <div class="line1"></div>
      <div class="line2"></div>
      <div class="line3"></div>
    </div>
  </nav>
</template>

<script>
import axios from 'axios';

export default {
  name: 'NavBar',
  data() {
    return {
      isNavActive: false,
      contactLinks: {}
    };
  },
  computed: {
    githubIcon() {
      return `${window.location.origin}/github-mark-white.svg`;
    },
    emailIcon() {
      return `${window.location.origin}/email.png`;
    }
  },
  created() {
    axios.get('/BlockchainsData.json').then(response => {
      this.contactLinks = response.data.contactLinks;
    }).catch(error => {
      console.error('Error fetching data:', error);
    });
  },
  methods: {
    toggleNav() {
      this.isNavActive = !this.isNavActive;
    },
    closeNav() {
      this.isNavActive = false;
    },
  },
};
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: transparent;
  width: 100%;
  position: fixed;
  top: 0;
  z-index: 1000;
  padding: 10px;
  box-sizing: border-box;
}

.logo {
  display: flex;
  flex-direction: column;
  align-items: left;
}

.links {
  display: flex;
  margin-left: auto;
}

.logo img {
  height: 40px;
}

.links img {
  height: 25px;
  margin: 0px 30px;
}

.logo p {
  color: rgba(255, 255, 255, 0.7);
  margin: 5px 0 0;
  font-size: 12px;
  font-weight: bold;
  text-align: center;
}

.nav-links {
  list-style: none;
  display: flex;
  margin: 0;
  padding: 0;
}

.nav-links li {
  margin-left: 20px;
}

.nav-links li a {
  color: #ffffff;
  text-decoration: none;
  padding: 8px 10px;
  font-size: 14px;
  font-weight: bold;
  transition: background-color 0.3s;
}

.nav-links li a:hover {
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 5px;
}

.burger {
  display: none;
  cursor: pointer;
  flex-direction: column;
}

.burger div {
  width: 25px;
  height: 3px;
  background: #fff;
  margin: 5px;
  transition: all 0.3s ease;
}

@media (max-width: 767.98px) {
  .nav-links {
    position: fixed;
    right: 0;
    top: 0;
    height: 100vh;
    background: rgba(0, 0, 0, 0.9);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    transform: translateX(100%);
    transition: transform 0.3s ease-in-out;
    z-index: 999;
    visibility: hidden;
  }

  .nav-links.nav-active {
    transform: translateX(0);
    visibility: visible;
  }

  .nav-links li {
    margin-top: 20px;
  }

  .burger {
    display: flex;
  }

  .logo img {
    height: 30px;
  }

  .links img {
  height: 20px;
  margin: 0px 20px;
}

  .logo p {
    font-size: 0.5em;
  }
}

@media (min-width: 768px) and (max-width: 991.98px) {
  .navbar {
    padding: 15px;
  }

  .logo img {
    height: 35px;
  }

  .logo p {
    font-size: 0.6em;
  }

  .nav-links {
    flex-wrap: wrap;
    justify-content: center;
  }

  .nav-links li {
    margin: 0 5px;
  }

  .nav-links li a {
    font-size: 12px;
    padding: 6px 8px;
  }
}

@media (min-width: 992px) {
  .navbar {
    padding: 20px;
  }

  .logo img {
    height: 50px;
  }

  .logo p {
    font-size: 0.8em;
  }

  .nav-links li {
    margin: 0 10px;
  }

  .nav-links li a {
    font-size: 16px;
    padding: 10px 12px;
  }
}
</style>
