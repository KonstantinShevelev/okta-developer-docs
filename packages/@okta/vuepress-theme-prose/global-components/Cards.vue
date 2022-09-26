<template>
  <div class="cards-own">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    methods: {
      isEqual(a, b) {
        return a === b;
      }
    },

    mounted() {
      window.addEventListener("load", () => {
         const cardsOwn = document.querySelectorAll(".cards-own");

         cardsOwn.forEach(card => {
            const cards = card.children;
            const cardsLength = cards.length;

            if (this.isEqual(cardsLength, 1)) {
              card.classList.add("cards-own_type_secondary");
            }
         });
      })
    }
  }
</script>
