<template>
  <section v-if="$store.state.allStaff">
    <b-container>
      <TitleSection title="Наши врачи" btn-link="/" />
      <b-row>
        <b-col class="slider-wrapper">
          <SliderCarousel :slides="$store.state.allStaff.slice(0, 10)" type="staff" />
        </b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'SectionStaff',
  async fetch() {
    if (!this.$store.state.allStaff) {
      const { data: allStaff } = await axios.get(
        `${process.env.VUE_APP_WP_API_URL}/wp/v2/staff?per_page=99`
      )
      this.$store.commit('SET_ALL_STAFF', allStaff)
    }
  },
}
</script>
<style lang="sass" scoped>
section
  background-color: var(--bg-soft)
</style>
