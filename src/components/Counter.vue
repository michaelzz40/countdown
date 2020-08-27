<template>
  <div class="counter-section">
    <section class="time text-6xl flex justify-center content-center" v-if="loaded">
      <div class="days mr-2 relative">
        {{ displayDays }}
        <div class="label text-sm absolute bottom-0">days</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="hours mx-2 relative">
        {{ displayHours }}
        <div class="label text-sm absolute bottom-0">hours</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="minutes mx-2 relative">
        {{ displayMinutes }}
        <div class="label text-sm absolute bottom-0">hours</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="seconds mx-2 relative">
        {{ displaySeconds }}
        <div class="label text-sm absolute bottom-0">hours</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      loaded: false,
      expired: false,
      appear: false
    };
  },
  props: ["year", "month", "date", "hour", "minute", "second", "millisecond"],
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60;
    },

    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
    end() {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond
      );
    }
  },
  mounted() {
    this.showRemaining();
  },
  methods: {
    formatNum(num) {
      return num < 10 ? "0" + num : num;
    },
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();

        // const end = new Date(2020, 11, 31, 0, 0, 0, 0);
        const distance = this.end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          this.expired = true;
          this.year += 1;
          return;
        }

        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.displayMinutes = this.formatNum(minutes);
        this.displaySeconds = this.formatNum(seconds);
        this.displayHours = this.formatNum(hours);
        this.displayDays = this.formatNum(days);
        this.loaded = true;
      }, 1000);
    }
  }
};
</script>

<style scoped>
.counter-section {
  margin-top: 3em;
  padding: 6em 3em 2em;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  animation: 2s fadeIn 3s ease forwards;
}

.seconds {
  max-width: 60px;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>