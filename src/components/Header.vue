<template>
  <header>
    <div class="header-container">
      <div class="logo-container">
        <img class="logo" src="../assets/imgon.png" alt="" />
      </div>

      <nav>
        <div class="nav-content">
          <a @click="goToMain" href="#">Home</a>
          <a @click="goToAbout" href="#">About</a>
        </div>
      </nav>
    </div>
  </header>
</template>

<script>
import { defineComponent } from "vue";
import { useRouter } from "vue-router";
export default defineComponent({
  setup() {
    const router = useRouter();

    const goToMain = () => {
      router.push({ name: "Main" });
    };

    const goToAbout = () => {
      router.push({ name: "About" });
    };

    return {
      goToMain,
      goToAbout,
    };
  },
});
</script>

<style scoped>
.logo-container {
  display: flex;
}
.logo {
  width: 60%;
}
.header-container {
  font-size: 26px;
  background-color: #aee5ff;
  display: grid;
  grid-template-columns: repeat(2, auto);
  align-items: center;
  justify-content: space-around;
}

.nav-content {
  display: grid;
  grid-template-columns: repeat(2, auto);
  align-items: center;
  gap: 50px;
}
.nav-content a {
  color: black;
}
</style>
