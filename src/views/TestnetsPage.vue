<template>
  <div class="testnets">
    <h2>Testnets</h2>
    <p>We validate</p>
    <div class="testnets-list">
      <a v-for="blockchain in testnets" :key="blockchain.name" :href="blockchain.developerLink" class="blockchain-link"
        target="_blank" rel="noopener noreferrer">
        <div class="blockchain">
          <img :src="blockchain.logo" :alt="blockchain.name">
          <div class="blockchain-details">
            <h3>{{ blockchain.name }}</h3>
            <p>{{ blockchain.description }}</p>
          </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'TestnetsPage',
  data() {
    return {
      testnets: []
    };
  },
  created() {
    axios.get('/BlockchainsData.json')
      .then(response => {
        this.testnets = response.data.blockchains.filter(bc => !bc.mainnet);
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  }
}
</script>

<style scoped>
.testnets {
  text-align: center;
  padding: 20px;
  background-color: rgba(0, 0, 0, 0.7);
  border-radius: 10px;
}

.testnets-list {
  max-height: 350px;
  /* Adjust height as needed */
  overflow-y: auto;
  margin-top: 20px;
  padding-right: 10px;
  background-color: rgba(102, 81, 153, 0.1);
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* Center the blocks */
}

/* Custom scrollbar styles */
.testnets-list::-webkit-scrollbar {
  width: 10px;
}

.testnets-list::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
}

.testnets-list::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.5);
  border-radius: 10px;
  border: 2px solid rgba(255, 255, 255, 0.1);
}

.testnets-list::-webkit-scrollbar-thumb:hover {
  background: rgba(0, 0, 0, 0.7);
}

.blockchain-link {
  text-decoration: none;
  color: inherit;
  /* Ensures the text color inherits from the parent */
  width: 100%;
  /* Ensure links take full width */
  display: flex;
  justify-content: center;
  /* Center the blocks */
}

.blockchain {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  padding: 10px;
  background-color: rgba(0, 0, 0, 0.8);
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
  width: 90%;
  /* Fixed width for better alignment */
  max-width: 700px;
  /* Optional: Set a max width */
}

.blockchain:hover {
  transform: scale(1.05);
}

.blockchain img {
  width: 50px;
  height: 50px;
  margin-right: 20px;
  border-radius: 50%;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
}

.blockchain-details {
  text-align: left;
  color: #ffffff;
  max-width: 70%;
  word-wrap: break-word;
  margin-bottom: 20px;
}

.blockchain p {
  margin: 0;
  white-space: pre-line;
  /* Allow wrapping */
}

/* Responsive styles */
@media (max-width: 767.98px) {
  .testnets {
    padding: 10px;
  }

  .testnets-list {
    max-height: 400px;
    padding: 10px;
  }

  .blockchain {
    width: 90%;
    flex-direction: column;
    align-items: center;
  }

  .blockchain img {
    margin: 0;
  }

  .blockchain-details {
    max-width: 100%;
    text-align: center;
  }

  h2 {
    font-size: 1em;
  }

  p {
    font-size: 0.8em;
  }

  .blockchain-details h3 {
    font-size: 0.8em;
  }

  .blockchain-details p {
    font-size: 0.7em;
  }

  .blockchain img {
    width: 30px;
    height: 30px;
  }
}

@media (min-width: 768px) and (max-width: 991.98px) {
  .testnets {
    padding: 10px;
  }

  .testnets-list {
    max-height: 350px;
  }

  .blockchain-link {
    width: 90%;
    margin: 5px;
  }

  h2 {
    font-size: 1.25em;
  }

  p {
    font-size: 1em;
  }

  .blockchain-details h3 {
    font-size: 1.125em;
  }

  .blockchain-details p {
    font-size: 1em;
  }

  .blockchain img {
    width: 40px;
    height: 40px;
  }
}

@media (min-width: 992px) and (max-width: 1199.98px) {
  .testnets {
    padding: 10x;
  }

  .blockchain-link {
    width: 95%;
    margin: 5px;
  }

  h2 {
    font-size: 1.5em;
  }

  p {
    font-size: 1em;
  }

  .blockchain-details h3 {
    font-size: 1.25em;
  }

  .blockchain-details p {
    font-size: 1em;
  }
}

@media (min-width: 1200px) {
  .testnets {
    padding: 30px;
  }

  .testnets-list {
    max-height: 400px;
  }

  .blockchain-link {
    width: 95%;
    margin: 10px;
  }

  h2 {
    font-size: 1.5em;
  }

  p {
    font-size: 1em;
  }

  .blockchain-details h3 {
    font-size: 1.25em;
  }

  .blockchain-details p {
    font-size: 1em;
  }
}
</style>