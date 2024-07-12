
<template>
  <div id="app">
    <div class="section users_list">
      <div class="users_list_header">
        <p>Profiles List</p>
        <div class="buttons">
          <button @click="sortAsc">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <polyline points="18 15 12 9 6 15" />
            </svg>
          </button>
          <button @click="sortDesc">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <polyline points="18 15 12 9 6 15" />
            </svg>
          </button>
        </div>
      </div>
      <input v-model="search" @input="filterProfiles" class="input" placeholder="Find Profile">

      <ProfileCard
        v-for="profile in displayedProfiles"
        :key="profile.id"
        :profile="profile"
        class="profile"
      />
    </div>

    <div class="section add_profile">
      <p >Add new profile</p>
      <div class="flex-row">
        <label class="label">Name:</label>
        <input v-model="newProfile.name" class="input">
      </div>
      <div class="flex-row">
        <label class="label" for="filter">Email:</label>
        <input v-model="newProfile.email" class="input">
      </div>
      <div class="flex-row">
        <label class="label">Specialisation:</label>
        <input v-model="newProfile.description" class="input">
      </div>
      <button @click="addProfile">Add</button>
    </div>
  </div>
</template>

<script>
import ProfileCard from "./components/ProfileCard.vue";

export default {
  name: "App",

  components: {
    ProfileCard
  },

  data() {
    return {
      profiles: [
        {
          id: 1,
          name: "Wojciech",
          email: "wojciech@poz.pl",
          description: "Anaesthesiologist",
          likes: 34
        },
        {
          id: 2,
          name: "Maria",
          email: "maria@poz.pl",
          description: "Radiologist",
          likes: 28
        },
        {
          id: 3,
          name: "Anna",
          email: "anna@poz.pl",
          description: "Surgeon",
          likes: 53
        }
      ],
      newProfile: {
        name: "",
        email: "",
        description: "",
        likes: 0,
        comment: ""
      },
      search: "",
    };
  },
  computed: {
    filteredProfiles() {
      return this.profiles.filter(profile => {
        return (
          profile.name.toLowerCase().includes(this.search.toLowerCase()) ||
          profile.email.toLowerCase().includes(this.search.toLowerCase())
        );
      });
    },

    displayedProfiles() {
      return this.search ? this.filteredProfiles : this.profiles;
    }
  },
  methods: {
    sortAsc() {
      this.profiles.sort(function(a, b) {
        return a.likes - b.likes;
      });
    },

    sortDesc() {
      this.profiles.sort(function(a, b) {
        return b.likes - a.likes;
      });
    },
    addProfile() {
      if (
        this.newProfile.name &&
        this.newProfile.email &&
        this.newProfile.description
      ) {
        const newId = this.profiles.length
          ? this.profiles[this.profiles.length - 1].id + 1
          : 1;
        this.profiles.unshift({
          ...this.newProfile,
          id: newId
        });
        this.newProfile = {
          name: "",
          email: "",
          description: "",
          likes: 0,
          comment: ""
        };
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Roboto", helvetica, arial, sans-serif;
  text-align: center;
  color: black;
  padding: 10px;
  display: flex;
  align-items: flex-start;
  justify-content: space-around;
  position: relative;
  font-size: 1.5em;
}

button {
  display: block;
  padding: 1em;
  width: 100%;
  background-color: #6982FD;
  border: 1px solid;
  color: #fff;
  cursor: pointer;
  font-weight: 600;
  text-shadow: 0 1px 0 rgba(black, 0.2);
  border-radius: 16px;
}

.section {
  min-width: 300px;
  padding: 2em;
  position: relative;
  border-radius: 20px;
}

.section p {
  margin-bottom: 0.5em;
}

.users_list_header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.buttons {
  display: flex;
}

.buttons button {
  width: 35px;
  height: 35px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  background: rgba(74, 109, 255,.3);
  color: rgba(74, 109, 255, 1) !important;
  cursor: pointer;
  padding: .45rem;
}

.buttons button:first-child {
  margin-right: 8px;
  transform: rotate(180deg);
}

.users_list p {
  text-align: left;
  font-weight: 600;
  margin: 0;
}

.users_list input {
  width: 100%;
  border-radius: 8px;
  transition: all .4s;
  padding: 1em;
  border: 0;
  color: #8f8f8f;
  font-size: 1rem;
  filter: grayscale(1);
}

.users_list input:focus {
  outline: none;
  box-shadow: 0 0 15px rgba(0,0,0,.09);
}

.add_profile {
  border: 1px solid #e6e6e6;
  color: #000;
  text-align: left;
  position: sticky;
  top: 20px;
  padding: 2rem;
  margin-top: 70px;
}

.add_profile p {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 2rem;
}

.add_profile input {
  width: 100%;
  border-radius: 8px;
  transition: all .4s;
  padding: 1em;
  border: 0;
  color: #8f8f8f;
  font-size: 1rem;
}

.add_profile input:focus {
  outline: none;
  box-shadow: 0 0 15px rgba(0,0,0,.09);
}

.label {
  width: 160px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  font-size: 14px;
  font-weight: 600;
}


@media (min-width: 600px) {
  .section {
    width: 50vw;
    max-width: 18em;
  }
}

.flex-row {
  display: flex;
  margin-bottom: 1em;
}


.profile {
  margin-top: 20px;
}

.icons-note {
  margin-top: 30px;
  font-size: 10px;
}

@media (max-width: 1200px) {
  #app {
    padding: 10px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .section {
    min-width: 360px;
    padding: 0;
    margin: 0 !important;
  }

  .buttons button {
    width: 30px;
    height: 30px;
  }

  .add_profile {
    position: relative;
    padding: 1rem;
    width: 90%;
    margin: 1rem auto !important;
  }

  .add_profile p {
    font-size: 1.1rem;
    font-weight: 600;
    margin-bottom: 2rem;
  }

  .flex-row {
    flex-direction: column;
    margin-bottom: 1rem;
  }

  .label {
    width: auto;
    font-size: 1rem;
    margin-bottom: .4rem;
  }
}
</style>
