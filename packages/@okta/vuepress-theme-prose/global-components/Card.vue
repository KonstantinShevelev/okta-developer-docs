<template>
  <SmartLink
    :item="{ link: href }"
    :class="type ? 'card_type_secondary' : ''"
    classes="card is-card-action is-card-clickable"
  >
    <header class="card--header">
      <figure
        v-if="headerIcon"
        class="card--header-icon"
      >
        <i
          class="icon-75"
          :class="headerIcon"
        ></i>
      </figure>
      <figure
        v-else-if="checkImageExists(headerImage)"
        class="card--header-icon"
      >
        <div>
          <img
            class="card--header-img"
            :src="headerImage"
          />
        </div>
      </figure>
      <section class="card--header-main-own">
        <h2
          v-if="cardTitle"
          class="card--title"
        >
          {{ cardTitle }}
        </h2>
        <section
          v-if="cardMeta"
          class="card--meta"
        >
          {{ cardMeta }}
        </section>
      </section>
    </header>
    <section class="card--main">
      <p>
        <slot>
          Commodo deserunt nulla Lorem veniam do minim consectetur ea in.
        </slot>
        <span
          v-if="type === 'secondary'"
          class="card__link"
        >
          Learn more
        </span>
      </p>
    </section>
    <footer
      v-if="showFooter"
      class="card--footer"
    >
      <section class="card--actions">
        <span class="card--link">
          {{ cardLinkText }}
        </span>
      </section>
    </footer>
  </SmartLink>
</template>

<script>
export default {
    components: {
        SmartLink: () => import("../components/SmartLink.vue")
    },
    props: {
        type: {
          default: "",
          type: String,
        },
        href: {
            default: "#",
            type: String,
        },
        headerIcon: {
            default: null,
            type: String,
        },
        headerImage: {
            default: null,
            type: String,
        },
        cardTitle: {
            default: "",
            type: String,
        },
        cardMeta: {
            default: "",
            type: String,
        },
        cardLinkText: {
            default: "Read More",
            type: String,
        },
        showFooter: {
            default: false,
            type: Boolean,
        },
    },
    methods: {
      isURLAbsolute(URL) {
        return URL.indexOf('://') > 0 ||
               URL.indexOf('//') === 0
      },

      checkImageExists(imageURL) {
        const isImageURLRelative =
          !this.isURLAbsolute(imageURL) ?
            `${location.origin}${imageURL}` : null;

        const http = new XMLHttpRequest();

        http.open('HEAD', isImageURLRelative || imageURL, false);
        http.send();

        return http.status != 404;
      }
    }
};
</script>

<style scoped></style>
