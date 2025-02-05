<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname">{{ person.name.first }} {{ person.name.last }}</div>
      <div class="banner__position">{{ person.position }}</div>
      <div class="banner__years">{{ person.years }}</div>
    </div>

    <div class="content">
      <div class="content__left">

        <div class="section">
          <div class="section-headline">
            {{ lang.contact }}
          </div>

          <div class="section-content section-content--plain">

            <a
              class="section-link"
              :href="contactLinks.email">
              <i class="section-link__icon material-icons">mail</i>{{ person.contact.email }}
            </a>

            <div class="section-link">
              <i class="section-link__icon material-icons">phone</i>{{ person.contact.phone }}
            </div>

            <a
              v-if="person.contact.website"
              class="section-link"
              :href="person.contact.website">
              <i class="section-link__icon fa fa-globe"></i>{{ person.contact.website }}
            </a>

            <a
              v-if="person.contact.linkedin"
              class="section-link"
              :href="contactLinks.linkedin">
              <i class="section-link__icon fa fa-linkedin"></i>{{ person.contact.linkedin }}
            </a>

            <a
              v-if="person.contact.github"
              class="section-link"
              :href="contactLinks.github">
              <i class="section-link__icon fa fa-github"></i>{{ person.contact.github }}
            </a>

            <a
              v-if="person.contact.medium"
              class="section-link"
              :href="contactLinks.medium">
              <i class="section-link__icon fa fa-medium"></i>{{ person.contact.medium }}
            </a>
          </div>
        </div>
        <br/>
        <div class="section">
          <div class="section-headline">
            {{ lang.about }}
          </div>
          <div class="section-content section-content--plain">
            <span class="section-content__pre">{{ person.about }}</span>
          </div>
        </div>
        <br/>
        <div
          v-if="person.skillcategories"
          class="section">
          <div class="section-headline">
            {{ lang.skills }}
          </div>

          <div
            v-for="(skillcategory, categoryindex) in person.skillcategories"
            class="section-content-grid"
            :key="categoryindex"
          >
            <a
              v-for="(skill, skillindex) in skillcategory.skills"
              class="grid-item"
              :key="skillindex"
              :href="skill.url">
              <span class="squarred-grid-item">
                {{ skill.name }}
              </span>
            </a>
          </div>
        </div>

      </div>

      <div class="content__right">
        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">work</i>{{ lang.experience }}
          </div>

          <div class="section-content">
            <a
              v-for="(experience, index) in person.experience"
              :key="index"
              class="section-content__item"
              :href="experience.website">

              <span class="section-content__header section-content__listheader">{{ experience.position }}</span>
              <span class="section-content__subheader">
                {{ experience.company }}
                <span class="section-content__plain">{{ experience.location }}</span>
              </span>

              <div class="section-content__text">{{ experience.timeperiod }}</div>
              <div class="section-content__text--light section-content__pre">{{ experience.description }}</div>
              <div class="section-subcontent__text--light">{{ experience.techno }}</div>

              <div
                v-for="(mission, missionindex) in experience.mission"
                :key="missionindex"
                class="section-subcontent"
              >
                <span class="section-subcontent__header">
                  {{ mission.client }} : {{ mission.missiondescription }}
                </span>
                <div class="section-subcontent__text--light">
                  {{ mission.missiontechno }}
                </div>
              </div>
            </a>
          </div>
        </div>
        <div
          v-if="person.education"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">school</i>{{ lang.education }}
          </div>

          <div class="section-content">
            <a
              v-for="(education, index) in person.education"
              class="section-content__item"
              :key="index"
              :href="education.url">
              <span class="section-content__header">{{ education.degree }} - <span class="section-content__headerlabel">{{ education.desc }}</span></span>
            </a>
          </div>
        </div>

        <div
          v-if="person.hobbies"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon fa fa-heart"></i>{{lang.hobbies}}
          </div>

          <div class="section-content">
            <a
              v-for="(hobbie, index) in person.hobbies"
              class="section-content__item"
              :key="index"
              :href="hobbie.url">
              <span class="section-content__header">{{ hobbie.name }} - <span class="section-content__headerlabel">{{ hobbie.description }}</span></span>
            </a>
          </div>
        </div>
      </div>
    </div>

    <img class="picture"/>
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'teuteuf-cool';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@accent-color: #0b2027;
@banner-color: #40798c;
@banner-height: 80px;
@picture-size: 120px;
@picture-offset: 35px;
@base-padding: 30px;
@left-column-width: 240px;

a {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
  }
}

.resume {
  position: relative;
  font-family:'Roboto' !important;
  font-size: 0.9em;
}

.picture {
  position: absolute;
  top: @banner-height - @picture-offset;
  left: @left-column-width + @base-padding * 2 - @picture-size / 2;
  height: @picture-size;
  width: @picture-size;
  border-radius: 50%;
  border: 5px solid @accent-color;
  content: url('../../resume/id.jpg');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;
  /*
    background-image: url('../../resume/banner.png');
    background-repeat: no-repeat;
    background-size: cover;
  */
  color: white;

  &__fullname {
    font-size: 32px;
  }

  &__position {
    font-size: 16px;
  }

  &__years {
    margin-top: 4px;
    font-size: 14px;
  }

  &__location {
    margin-top: 5px;
    font-size: 12px;
  }
}

.content {
  display: flex;
  width: 100%;
  height: 100%;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
  }

  &__left {
    width: @left-column-width;
    color: rgba(255, 255, 255, 0.59);
    background-color: @accent-color;

    .section-headline {
      color: white;
    }
  }

  &__right {
    flex: 1;
  }
}

.section {
  margin: 5px 0 10px 0;
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin: 8px 0;

  &__icon {
    margin-right: 8px;
    font-size: 1.4em;
  }
}

.section-link {
  font-size: 1.1em;
  color: rgba(255, 255, 255, 0.59) !important;

  &__icon {
    color: white;
  }
}

.section-content {
  margin-top: 5px;
  padding-left: 32px;
  font-size: 14px;

  &__pre {
    white-space: pre-line;
  }

  &__item {
    display: block;
    margin-bottom: 5px;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__listheader {
    margin-top: 12px;
  }

  &__headerlabel {
    font-size: 0.8em;
    font-weight: normal;
  }

  &__subheader {
    display: block;
    font-weight: 400;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
      white-space: pre-line;
      margin: 0.5em 0;
    }
  }

  &__plain {
    display: inline;
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }

  &--justify {
    text-align: justify;
  }
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 5px;
  margin-bottom: 5px;
}

.section-subcontent {
  margin: 10px 0 10px 10px;

  &__header {
    display: block;
    font-size: 12px;
    font-weight: 500;
  }

  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
      font-style: italic;
    }
  }
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item {
  display: block;
  border: 1px solid white;
  color: white;
  margin-top: 5px;
  padding: 5px;
}
</style>
