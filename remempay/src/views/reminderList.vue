<template>
  <div>
    <Navbar></Navbar><br /><br />
    <h1>Reminder List</h1>
    <div id="home-page">
      <div class="row flex justify-content-center">
        <div class="card col-4 m-2" v-for="data in reminder" :key="data.id">
          <div class="card-body text-center">
            <h5>Payment for:</h5>
            <h5 class="card-title">{{ data.receiver.name }}</h5>
            <h5>Payment amount</h5>
            <h5>{{ data.amount }}</h5>
            <h5>Paid Amount:</h5>
            <h5>{{ data.paid }}</h5>
            <h5>Payment deadline:</h5>
            <h5>{{ convertDate(data.deadline) }}</h5>
            <button type="button" class="rounded" v-on:click="pay(data.id)">
              <span>Pay</span>
            </button>
          </div>
        </div>
      </div>
    </div>
    <HFooter></HFooter>
  </div>
</template>

<script>
import dayjs from "dayjs";
import HFooter from "vue-hacktiv8-footer";
import Navbar from "../components/Navbar.vue";
export default {
  name: "Reminder",
  components: {
    Navbar,
    HFooter,
  },
  computed: {
    reminder() {
      return this.$store.state.reminder;
    },
  },
  methods: {
    convertDate: function (date) {
      return dayjs(date).format("DD-MMM-YYYY");
    },
    pay: function (id) {
      this.$store.dispatch("storeReminder", id);
      this.$router.push("/pay");
    },
  },
  created() {
    this.$store.dispatch("fetchReminder");
  },
};
</script>

<style></style>
