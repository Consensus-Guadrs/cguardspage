<template>
  <div class="community-contributions">
    <h2>Community Contributions</h2>
    <div class="contributions-list">
      <a v-for="(contribution, index) in contributions" :key="index" :href="contribution.link" target="_blank"
        class="contribution-link">
        <div class="contribution">
          <img :src="contribution.logo" :alt="contribution.description">
          <div class="contribution-details">
            <p>{{ contribution.description }}</p>
          </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'CommunityContributionsPage',
  data() {
    return {
      contributions: []
    };
  },
  created() {
    axios.get('/BlockchainsData.json')
      .then(response => {
        this.contributions = response.data.communityContributions;
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  }
}
</script>

<style scoped>
.community-contributions {
  text-align: center;
  padding: 20px;
  background-color: rgba(0, 0, 0, 0.7);
  border-radius: 10px;
}

.contributions-list {
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
.contributions-list::-webkit-scrollbar {
  width: 10px;
}

.contributions-list::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
}

.contributions-list::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.5);
  border-radius: 10px;
  border: 2px solid rgba(255, 255, 255, 0.1);
}

.contributions-list::-webkit-scrollbar-thumb:hover {
  background: rgba(0, 0, 0, 0.7);
}

.contribution-link {
  text-decoration: none;
  color: inherit;
  /* Ensures the text color inherits from the parent */
  width: 100%;
  /* Ensure links take full width */
  display: flex;
  justify-content: center;
  /* Center the blocks */
}

.contribution {
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

.contribution:hover {
  transform: scale(1.05);
}

.contribution img {
  width: 50px;
  height: 50px;
  margin-right: 20px;
  border-radius: 50%;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
}

.contribution-details {
  text-align: left;
  color: #ffffff;
  max-width: 70%;
  /* Set a maximum width for the details */
  word-wrap: break-word;
  /* Break long words */
}

.contribution p {
  margin: 0;
  white-space: pre-line;
  /* Allow wrapping */
}

/* Responsive styles */
@media (max-width: 767.98px) {
  .contributions {
    padding: 10px;
  }

  .contributions-list {
    max-height: 400px;
    padding: 10px;
  }

  .contribution {
    width: 90%;
    flex-direction: column;
    align-items: center;
  }

  .contribution img {
    margin: 0;
  }

  .contribution-details {
    max-width: 100%;
    text-align: center;
  }

  h2 {
    font-size: 1em;
  }

  p {
    font-size: 0.8em;
  }

  .contribution-details h3 {
    font-size: 0.8em;
  }

  .contribution-details p {
    font-size: 0.7em;
  }

  .contribution img {
    width: 30px;
    height: 30px;
  }
}

@media (min-width: 768px) and (max-width: 991.98px) {
  .contributions {
    padding: 10px;
  }

  .contributions-list {
    max-height: 350px;
  }

  .contribution-link {
    width: 90%;
    margin: 5px;
  }

  h2 {
    font-size: 1.25em;
  }

  p {
    font-size: 1em;
  }

  .contribution-details h3 {
    font-size: 1.125em;
  }

  .contribution-details p {
    font-size: 1em;
  }

  .contribution img {
    width: 40px;
    height: 40px;
  }
}

@media (min-width: 992px) and (max-width: 1199.98px) {
  .contributions {
    padding: 10x;
  }

  .contribution-link {
    width: 95%;
    margin: 5px;
  }

  h2 {
    font-size: 1.5em;
  }

  p {
    font-size: 1em;
  }

  .contribution-details h3 {
    font-size: 1.25em;
  }

  .contribution-details p {
    font-size: 1em;
  }
}

@media (min-width: 1200px) {
  .contributions {
    padding: 30px;
  }

  .contributions-list {
    max-height: 400px;
  }

  .contribution-link {
    width: 95%;
    margin: 10px;
  }

  h2 {
    font-size: 1.5em;
  }

  p {
    font-size: 1em;
  }

  .contribution-details h3 {
    font-size: 1.25em;
  }

  .contribution-details p {
    font-size: 1em;
  }
}
</style>
