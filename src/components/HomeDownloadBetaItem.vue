<template>
  <div class="download-beta-item">
    <a :href="github" @click="codeClick" class="code">{{ code }}</a>
    <a
      class="released"
      :title="releasedString"
      :href="`https://github.com/wulkanowy/wulkanowy/tree/${code}`"
      @click="releasedClick">
      {{ releasedRelativeString }}
    </a>
    <div class="buttons">
      <a
        class="github-button"
        :href="github"
        title="GitHub"
        @click="githubClick">
        <span class="mdi mdi-github-circle"></span>
      </a>
      <a
        class="download-button"
        :href="download"
        title="Pobierz"
        @click="downloadClick">
        <span class="mdi mdi-download"></span>
      </a>
    </div>
  </div>
</template>

<script>
  import moment from 'moment';

  moment.locale('pl');

  export default {
    name: 'home-download-beta-item',
    props: {
      code: {
        type: String,
      },
      released: {
        type: String,
      },
      github: {
        type: String,
      },
      download: {
        type: String,
      },
    },
    methods: {
      codeClick() {
        this.$ga.event({
          eventCategory: 'beta-item',
          eventAction: 'code-click',
          eventLabel: this.code,
        });
      },
      releasedClick() {
        this.$ga.event({
          eventCategory: 'beta-item',
          eventAction: 'released-click',
          eventLabel: this.code,
        });
      },
      githubClick() {
        this.$ga.event({
          eventCategory: 'beta-item',
          eventAction: 'github-click',
          eventLabel: this.code,
        });
      },
      downloadClick() {
        this.$ga.event({
          eventCategory: 'beta-item',
          eventAction: 'download-click',
          eventLabel: this.code,
        });
      },
    },
    computed: {
      releasedString() {
        return moment(this.released).format('dddd, D MMM YYYY HH:mm:ss');
      },
      releasedRelativeString() {
        const string = moment(this.released).fromNow();
        return string.charAt(0).toUpperCase() + string.slice(1);
      },
    },
  };
</script>

<style lang="scss" scoped>
  .download-beta-item {
    height: 56px;
    padding: 8px;
    display: grid;
    grid-template-rows: 1fr auto auto 1fr;
    grid-template-columns: 1fr auto;
    background-color: #fff;
    border-radius: 4px;
    font-family: 'Roboto', sans-serif;
    box-shadow: 0 3px 1px -2px rgba(0, 0, 0, 0.2),
      0 2px 2px 0 rgba(0, 0, 0, 0.14),
      0 1px 5px 0 rgba(0, 0, 0, 0.12);

    &:not(:first-child) {
      margin-top: 16px;
    }

    &:last-child {
      margin-bottom: 8px;
    }
  }

  .code {
    grid-column: 1;
    grid-row: 2;
    font-size: 24px;
    margin-bottom: 2px;
    color: #D32F2F;
    text-decoration: none;
    justify-self: start;

    &:hover {
      text-decoration: underline;
    }
  }

  .released {
    grid-column: 1;
    grid-row: 3;
    color: #0009;
    font-size: 14px;
    text-decoration: none;
    justify-self: start;

    &:hover {
      text-decoration: underline;
    }
  }

  .buttons {
    display: flex;
    flex-direction: row;
    grid-column: 2;
    grid-row: 1/5;

    .github-button, .download-button {
      font-size: 32px;
      color: #000;
      padding: 4px;
      margin: 4px 4px;
      display: block;
      align-self: center;
    }
  }
</style>
