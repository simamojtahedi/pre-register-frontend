<template>
  <div class="profile">
    <div class="card">
      <DoctorIcon class="avatar"/>
      <div class="data">
        <div class="profile-content">
          <div class="profile-info">
            <strong>{{profile.name}}</strong>
            <a :href="profile.email" class="email">{{profile.email}}</a>
          </div>
          <div class="description">{{profile.description}}</div>
        </div>
        <div class="likes">
          <span class="likes-icon">&#10084;</span>
          <span class="likes-value">{{profile.likes}}</span>
        </div>
      </div>
    </div>
    <div class="comment">
      <input class="comment-input" placeholder="Write your comment...">
    </div>
  </div>
</template>

<script>
import DoctorIcon from "./DoctorIcon.vue";

export default {
  name: "ProfileCard",

  components: {
    DoctorIcon
  },

  props: {
    profile: {
      type: Object,
      required: true
    }
  }
};
</script>

<style>
.card {
  display: flex;
  align-items: flex-start;
  padding: 10px;
  font-size: 14px;
  color: rgb(82, 82, 82);
  background-color: #fff;
  border-radius: 16px 16px 0 0;
  box-shadow: 0 0 15px rgba(0,0,0, .1);
}

.avatar {
  width: 64px;
  min-width: 64px;
  height: 64px;
  border: 1px solid rgb(172, 172, 172);
  border-radius: 100%;
}

.data {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 80%;
}

.profile-content {
  display: flex;
  flex-direction: column;
  text-align: left;
  margin-left: 15px;
  width: 100%;
}

.profile-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.profile-content strong {
  font-weight: 700;
  font-size: 1rem;
}

.email {
  color: rgba(74, 109, 255, 1);
  font-weight: 100;
}

.description {
  color: #777;
  margin: 0;
}

.likes {
  color: rgba(74, 109, 255, 1);
  margin-top: 10px;
  width: 100%;
  display: flex;
  justify-content: flex-end;
  margin-left: 10px;
}

.likes-value {
  margin-left: 5px;
}

.comment {
  display: flex;
  width: 100%;
}

.comment-input {
  width: 100%;
  border-radius: 0 0 16px 16px !important;
  padding: 8px;
  border: 0;
  box-shadow: 0 0 5px rgba(0,0,0,.03);
}
</style>
