<template>
  <article class="app-card">
    <div
      class="app-card__image"
      :lazy-background="image"
    />
    <div class="app-card__content">
      <header class="app-card__header">
        <h3 class="app-card__title">
          {{ title }}
        </h3>
        <div v-if="to" class="app-card__tags">
          <cv-tag
            v-for="tag in tags"
            :key="tag"
            :label="tag"
            kind="purple"
          />
        </div>
      </header>
      <div class="app-card__description">
        <slot />
      </div>
      <AppCta v-if="to" :url="to" class="app-card__link">
        {{ ctaLabel }}
      </AppCta>
    </div>
  </article>
</template>

<script lang="ts">
import Vue from 'vue'
import { Component, Prop } from 'vue-property-decorator'
import AppCta from '~/components/ui/AppCta.vue'

@Component({ components: { AppCta } })
export default class extends Vue {
  @Prop(String) image!: any
  @Prop(String) title!: any
  @Prop(Array) tags!: any
  @Prop(String) to!: any
  @Prop(String) ctaLabel!: any
}
</script>

<style lang="scss" scoped>
@import '~carbon-components/scss/globals/scss/typography';

.app-card {
  min-height: 13rem;
  width: 100%;
  background-color: $cool-gray-10;
  color: $cool-gray-80;
  display: flex;

  @include mq($until: medium) {
    height: auto;
    flex-direction: column;
  }

  &__image {
    flex: 0 0 14rem;
    background-color: $cool-gray-80;
    background-repeat: no-repeat;
    background-size: 100%;
    background-position: center;
    overflow: hidden;

    @include mq($from: medium, $until: large) {
      flex: 0 0 13rem;
    }

    @include mq($until: medium) {
      height: 13rem;
      width: auto;
    }
  }

  &__content {
    padding: $spacing-05 $spacing-05 $spacing-05 $spacing-07;
    display: flex;
    flex-direction: column;
  }

  &__header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;

    @include mq($until: large) {
      flex-direction: column;
    }
  }

  &__title {
    flex: 0 0 auto;
    @include type-style('productive-heading-02');
  }

   &__tags {
    width: 20rem;
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-end;

    @include mq($until: large) {
      justify-content: flex-start;
      margin-top: $spacing-03;
    }

    @include mq($from: medium, $until: large) {
      width: auto;
    }

    @include mq($until: medium) {
      width: 100%;
    }

    .bx--tag--purple {
      background-color: $purple-70;
      color: $white;
    }

    .bx--tag:first-child {
      margin-left: 0;
    }
  }

  &__description {
    @include type-style('body-long-01');
    margin-top: $layout-02;
    margin-bottom: $layout-02;
  }

  &__link {
    margin-top: auto;
  }
}
</style>
