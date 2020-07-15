<template>
  <div>
    <input type="text" size="10" v-model="value" />
    <input type="date" v-model="date" />
    <button v-on:click="save">Download</button>
    <svg
      width="512"
      height="512"
      fill="transparent"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      ref="stamp"
    >
      <g transform="translate(256, 256)" color="#dd4827" fill="none" stroke="currentColor">
        <g stroke-width="2pt">
          <circle r="250" stroke="currentColor" fill="none" />
          <line x1="-237" y1="-80" x2="237" y2="-80" />
          <line x1="-237" y1="80" x2="237" y2="80" />
        </g>
        <g transform="translate(0, 50)" fill="currentColor" font-size="100pt" text-anchor="middle">
          <text transform="translate(0, -150)" id="_family_name">{{ sir }}</text>
          <text transform="translate(0, 150)" id="_sir_name">{{ last }}</text>
          <text transform="scale(0.6, 1)" id="_date">{{ date }}</text>
        </g>
      </g>
    </svg>
  </div>
</template>

<script>
export default {
  name: "Stamp",
  props: {
    value: String,
  },
  computed: {
    sir: function () {
      return this.value.split(/\s/)[0];
    },
    last: function () {
      return this.value.split(/\s/)[1];
    },
  },
  data: function() {
    return {
      date: new Date(new Date().getTime() + 9 * 3600 * 1000).toISOString().substr(0, 10)
    };
  },
  methods: {
    save: function() {
      const canvas = document.createElement("canvas");
      canvas.setAttribute("width", 512);
      canvas.setAttribute("height", 512);
      const context = canvas.getContext("2d");

      const a = document.createElement("a");

      const image = new Image();
      image.addEventListener(
        "load",
        () => {
          context.drawImage(image, 0, 0);
          a.setAttribute("href", canvas.toDataURL("image/png"));
          a.setAttribute("download", `${this.value}_${this.date}.png`);
          a.click();
        },
        { once: true }
      );
      image.setAttribute(
        "src",
        "data:image/svg+xml;charset=utf-8;base64," +
          btoa(
            unescape(
              encodeURIComponent(
                new XMLSerializer().serializeToString(this.$refs.stamp)
              )
            )
          )
      );
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input, button {
  display: block;
  width: 10em;
  margin: 0.2em;
}

div {
  display: flex;
  flex-direction: column;
  margin: 1em auto;
  align-items: center;
}
</style>
