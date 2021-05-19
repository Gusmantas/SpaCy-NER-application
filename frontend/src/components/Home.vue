<template>
  <main>
    <form class="text-wrapper" @submit.prevent="submitText">
      <textarea v-model="text" name="" id="" cols="100" rows="10"></textarea>
      <div class="controls">
        <select v-model="selected" name="type">
          <option value="PERSON">Names</option>
          <option value="GPE">Places</option>
          <option value="ORG">Organizations</option>
          <option value="WORK_OF_ART">Art Titles</option>
          <option value="PRODUCT">Products</option>
        </select>
        <button type="submit">Submit</button>
      </div>
    </form>
    <div class="results" v-if="results">
      <p class="result" v-for="r of results" :key="r">{{ r }}</p>
    </div>

    <div class="texts">
      <p class="text" v-for="(text, i) of texts" :key="i">{{ text.text }}</p>
    </div>
  </main>
</template>

<script>
export default {
  created() {
    this.$store.dispatch("initTexts");
  },
  computed: {
    texts() {
      return this.$store.state.texts;
    },
  },
  data() {
    return {
      text: "",
      selected: "PERSON",
      results: "",
    };
  },
  methods: {
    async submitText() {
      const textObject = {
        text: this.text,
        type: this.selected,
      };

      if (!this.text) return;

      let text = await fetch("/api/texts", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(textObject),
      });

      if (text.ok) {
        text = await text.json();
        this.results = text;
        this.$store.commit("appendText", textObject);
      }
    },
  },
};
</script>

<style scoped>
.text-wrapper {
  display: flex;
  flex-direction: column;
  width: 50%;
  margin: 0 auto;
}

select,
button {
  margin: 15px 15px;
  width: 200px;
}

.results {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.result {
  margin: 3px;
  border: 1px solid rgb(27, 94, 27);
  background: rgb(212, 212, 106);
  padding: 5px;
  border-radius: 5px;
}

.texts {
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 100px;
}
.text {
  padding: 10px;
  border: 1px solid grey;
  width: 400px;
  max-height: 300px;
  overflow: auto;
  margin: 10px;
  border-radius: 8px;
  background-color: lightgray;
}

.text::-webkit-scrollbar {
  display: none;
}
</style>