<template>
  <div>
    <page-title back title="Coach Info"></page-title>

    <div class="container">
      <div class="coach">
        <div class="header">
          <div class="img-box">
            <img :src="selectedCoach.image" alt="Coach Photo" />
          </div>
          <div class="info-box">
            <div class="box-title">
              <p>Coach Profile</p>
            </div>
            <div class="coach-info">
              <p>
                name: <span>{{ selectedCoach.name }}</span>
              </p>
              <p>
                age: <span>{{ selectedCoach.age }}</span>
              </p>
              <p>
                Residence: <span>{{ selectedCoach.location }}</span>
              </p>
              <p>
                Email: <span>{{ selectedCoach.email }}</span>
              </p>
              <p>
                Website:
                <span>
                  <a :href="selectedCoach.website" v-if="actLink">{{
                    selectedCoach.website
                  }}</a>
                  <span v-else>{{ selectedCoach.website }}</span>
                </span>
              </p>
              <p>
                st. Phone: <span>{{ selectedCoach.phoneOne }}</span>
              </p>
              <p>
                nd. Phone: <span>{{ selectedCoach.phoneTow }}</span>
              </p>
              <p>
                Exeprince: <span>{{ selectedCoach.exp }}</span>
              </p>
              <p>
                Hourly Rate:
                <span> {{ selectedCoach.rate }} Dollars in Hour</span>
              </p>
              <p>
                Freelance:
                <span>{{
                  selectedCoach.freelance ? "Available" : "unavailable"
                }}</span>
              </p>
            </div>
          </div>
        </div>
        <div class="body">
          <div class="box-title">
            <p>Description</p>
          </div>
          <div class="content">{{ selectedCoach.disc }}</div>
          <div class="contact-btn">
            <button-base link :to="coachContactLink">Contact Coach</button-base>
            <span></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["id"],
  data() {
    return {
      selectedCoach: null,
    };
  },
  created() {
    this.selectedCoach = this.$store.getters["coaches/coaches"].find(
      (coach) => coach.id === this.id
    );
  },
  computed: {
    coachContactLink() {
      return "/coaches/" + this.id + "/contact";
    },
    actLink() {
      if (
        this.selectedCoach.website.includes("http") ||
        this.selectedCoach.website.includes("www")
      ) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
<style scoped>
.title {
  width: 100%;
  height: 60px;
  text-align: center;
  background-color: var(--b-color);
  color: #fff;
  font-size: var(--h2-fontSize);
  border-top: 0.5px solid gray;
  line-height: 60px;
}
.coach {
  width: 95%;
  margin: 25px auto;
  background-color: var(--b-color);
  color: #fff;
  border-radius: 15px;
}
.coach .header {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  margin-bottom: 10px;
}

.coach .header .img-box {
  width: 100%;
  position: relative;
  overflow: hidden;
}
.coach .header .img-box img {
  border-radius: 15px 0 0 0;
  width: 100%;
  max-height: 270px;
  height: auto;
}
.coach .header .info-box {
  padding: 5px 5px;
}
.coach .header .info-box p {
  margin: 3px 0;
}
.coach .box-title {
  font-size: var(--h3-font-size) !important;
  text-align: center;
  margin-bottom: 5px;
}
.coach .box-title p {
  border-bottom: 2px solid var(--y-color);
  display: inline-block;
}
.coach .coach-info p span,
.coach .coach-info p span a {
  color: var(--y-color);
  text-decoration: none;
}
.coach .body {
  padding: 10px;
}
.coach .body .contact-btn {
  width: 100%;
  margin: 10px;
  text-align: center;
}
@media (max-width: 590px) {
  .coach .header {
    grid-template-columns: repeat(1, 1fr);
  }
  .coach .header .img-box img {
    border-radius: 15px 15px 0 0;
    max-height: unset;
    height: auto;
  }
}
</style>