<template>
  <main class="content-status">
    <div>
      <div class="illustration">
        <img src="../assets/pencil-rocket.svg" />
      </div>

      <h2>{{ title }}</h2>
      <div v-if="issueUrl" class="content-status-status">
        <a target="_blank" :href="issueUrl">Check the status</a>
        of this page on GitHub.
      </div>
      <div class="section content-status-vote">
        <Feedback
          titleTxt="Is this topic important to you?"
          evtYes="topic_important"
          evtNo="topic_not_important"
          noTxt="Not really"
          yesTxt="Yes"
          :editOrIssueLinks="false"
        />
      </div>
      <div class="section content-status-info">
        <h3>Give us a hand</h3>
        <ul>
          <li v-if="issueUrl">
            <a target="_blank" :href="issueUrl">Help write this page</a>
          </li>
          <li v-if="$site.themeConfig.betaTestFormUrl">
            <a :href="$site.themeConfig.betaTestFormUrl" target="_blank"
              >Sign up to be a beta tester</a
            >
          </li>
        </ul>
      </div>
    </div>

    <div class="content-status-info" style="clear: both;">
      <div v-if="related" class="section content-other-resources">
        <h3>Other resources to try</h3>
        <ul>
          <li v-for="(item, title) in related">
            <a :href="item" :alt="title" target="_blank">{{ title }}</a>
          </li>
        </ul>
      </div>
    </div>
    <style>
      footer.page-edit {
        display: none;
      }
    </style>
  </main>
</template>

<script>
import Feedback from '../components/Feedback.vue'

export default {
  computed: {
    issueUrl: function () {
      return this.$frontmatter && this.$frontmatter.issueUrl
    },
    repo: function () {
      return (
        this.$site && this.$site.themeConfig && this.$site.themeConfig.docsRepo
      )
    },
    related: function () {
      return this.$frontmatter.related
    }
  },
  props: {
    title: {
      type: String,
      default: 'This content is still preparing for liftoff!'
    }
  },
  components: { Feedback }
}
</script>

<style lang="stylus" scoped>
h2, h3 {
  border-bottom: none;
  margin: 0.5rem 0; // TODO: make global
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;

  li {
    margin: 0;
    padding: 0;
  }
}

.content-status-vote {
  margin-top: 3rem;
}

.illustration {
  width: 20%;
  float: right;
}

// TODO: make global
.section {
  margin-bottom: 3rem;
}

@media (min-width: $MQNarrow) {
  .illustration {
    width: 40%;
    float: right;
  }
}
</style>
