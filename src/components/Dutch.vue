<template>
  <div class="container">
    <!-- persons -->
    <div class="persons">
      <!-- メンバーを追加 -->
      <ul class="p_list">
        <li v-for="(item, key) in data.arr" :key="key">
          <span>{{ key + 1 }}</span> - {{ item }}
        </li>
      </ul>

      <!-- メンバー追加フォーム -->
      <div class="p_form">
        <div class="p_form_item">
          <label for="name">Name:</label>
          <input type="text" v-model="data.person.name" />
        </div>
        <div class="p_form_item">
          <label for="color">Color:</label>
          <div id="pickr"></div>
        </div>
        <button v-if="data.p_add_flg === false" class="p_add_btn">add</button>
        <button v-else @click="p_add" class="p_add_btn active">add</button>
      </div>
    </div>

    <!-- // persons -->
    <div class="tasks"></div>
  </div>
</template>
<script>
import { reactive, onMounted, watchEffect } from "vue";
import "@simonwep/pickr/dist/themes/classic.min.css";
import Pickr from "@simonwep/pickr";

export default {
  setup() {
    const data = reactive({
      person: {
        name: "",
        color: "",
      },
      p_add_flg: false,
      arr: ["hoge", "fuga", "boke", "baz"],
    });

    const add_pickr = () => {
      const pickr = Pickr.create({
        el: "#pickr",
        theme: "classic",
        swatches: [
          "rgba(244, 67, 54, 1)",
          "rgba(233, 30, 99, 0.95)",
          "rgba(156, 39, 176, 0.9)",
          "rgba(103, 58, 183, 0.85)",
          "rgba(63, 81, 181, 0.8)",
          "rgba(33, 150, 243, 0.75)",
          "rgba(3, 169, 244, 0.7)",
          "rgba(0, 188, 212, 0.7)",
          "rgba(0, 150, 136, 0.75)",
          "rgba(76, 175, 80, 0.8)",
          "rgba(139, 195, 74, 0.85)",
          "rgba(205, 220, 57, 0.9)",
          "rgba(255, 235, 59, 0.95)",
          "rgba(255, 193, 7, 1)",
        ],
        components: {
          preview: true,
          opacity: true,
          hue: true,
          interaction: {
            hex: true,
            rgba: false,
            hsla: false,
            hsva: false,
            cmyk: false,
            input: true,
            clear: true,
            save: true,
          },
        },
      });
      pickr.on("save", (instance) => {
        data.person.color = instance.toHEXA().toString();
      });
    };

    watchEffect(() => {
      if (data.person.color && data.person.name) {
        data.p_add_flg = true;
      }
    })
    onMounted(() => {
      add_pickr();
    });
    return {
      data,
      add_pickr,
    };
  },
};
</script>
<style lang="scss" scoped>
@use "../assets/scss/variable" as v;

.container {
  max-width: 1000px;
  margin: 0 auto;
}

/**
* persons ****************************************************************************************************
**/
.persons {
  border: 1px solid transparent;
  margin: 50px auto 0;
  padding: 50px;
}
.p_list {
  width: 80%;
  margin: 50px auto;
  li {
    border: 2px solid v.$main_bg;
    margin-bottom: 10px;
    padding: 10px;
    span {
      color: v.$main_bg;
    }
  }
}

.p_add_btn{
  background-color: v.$main_bg;
  border: 2px solid v.$main_bg;
  color: white;
  transition: all .3s;
  opacity: .3;
  user-select: none;
}
.p_add_btn.active{
  opacity: 1;
  user-select: inherit;
  &:hover {
    background-color: white;
    color: v.$main_bg;
  }
}
.p_form {
  display: flex;
  justify-content: center;
  &_item {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-right: 20px;
  }
  label {
    margin-right: 10px;
  }
}
/**
* // persons ****************************************************************************************************
**/

.tasks {
  background-color: violet;
  height: 100px;
}
</style>
