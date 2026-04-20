<template>
  <div>
    <component :is="currentView"></component>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'
  import { types } from '../../../../../store'
  import ACMContestRank from './ACMContestRank.vue'
  import OIContestRank from './OIContestRank.vue'
  import CustomContestRank from './CustomContestRank.vue'

  const NullComponent = {
    name: 'null-component',
    template: '<div></div>'
  }

  export default {
    name: 'contest-rank',
    components: {
      ACMContestRank,
      OIContestRank,
      CustomContestRank,
      NullComponent
    },
    computed: {
      ...mapGetters(['contestRuleType']),
      currentView () {
        if (this.contestRuleType === null) {
          return 'NullComponent'
        }
        if (this.contestRuleType === 'ACM') {
          return 'ACMContestRank'
        } else if (this.contestRuleType === 'OI') {
          return 'OIContestRank'
        } else {
          return 'CustomContestRank'
        }
      }
    },
    beforeRouteLeave (to, from, next) {
      this.$store.commit(types.CHANGE_CONTEST_ITEM_VISIBLE, {menu: true})
      next()
    }
  }
</script>
<style lang="less" scoped>
</style>
