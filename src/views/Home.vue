<script setup>
import { ref } from "vue";

const color = ref("dark");
</script>

<template>
  <div class="home" :class="color == 'dark' ? 'home--dark' : ''">
    <div class="frame">
      <div class="name-container">
        <div>
          <div class="name" data-text="Piotr Błaszczak">Piotr Błaszczak</div>
          <div class="sub" data-text="Front-end Developer">
            Web Developer & Designer
          </div>
        </div>

        <ul class="menu">
          <li>
            <!-- Home -->
            <div class="dott"></div>
          </li>
          <li>Technologies</li>
          <li>Projects</li>
          <li>Contact</li>
        </ul>
      </div>

      <div class="desc">
        HI! My name is Piotr. <br />
        I'm a Web Devloper mainly working <br />
        with Vue.js and C# .NET. <br />
        I'm also a designer and I love to create <br />
        beautiful and useful web applications. <br />
        I'm currently working in <br />
        one of the Warsaw sofwere houses <br />
        and looking for new opportunities. <br />
        I'm also freelancer and I'm open to <br />
        new projects. <br />
        I'm studying Computer Science at the <br />
        PJATK University in Warsaw. <br />
        Feel free to contact me!
      </div>

      <div class="theme-swithcer">
        <div
          class="light"
          :class="color == 'light' ? 'light--checked' : ''"
          @click="color = 'light'"
        >
          <div class="box"></div>
          Light
        </div>
        <div
          class="dark"
          :class="color == 'dark' ? 'dark--checked' : ''"
          @click="color = 'dark'"
        >
          <div class="box"></div>
          Dark
        </div>
      </div>
    </div>
    <div class="copy">&#169; 2025 Piotr Błaszczak</div>
  </div>
</template>

<style lang="scss" scoped>
@keyframes bganimation {
  0% {
    background-position: -100% -100%, 200% 200%, -100% 200%, 200% -100%;
  }
  50% {
    background-position: 150% 100%, -200% 100%, 100% 0%, 0% 100%;
  }
  100% {
    background-position: -100% -100%, 200% 200%, -100% 200%, 200% -100%;
  }
}

.home {
  background: radial-gradient(
      ellipse at center,
      rgba(0, 0, 255, 0.3) 0%,
      rgba(0, 0, 0, 0) 70%
    ),
    radial-gradient(
      ellipse at center,
      rgba(255, 0, 0, 0.3) 0%,
      rgba(0, 0, 0, 0) 70%
    ),
    radial-gradient(
        ellipse at center,
        rgba(0, 255, 0, 0.3) 0%,
        rgba(0, 0, 0, 0) 70%
      )
      #e1eff1;
  background-repeat: no-repeat, no-repeat, no-repeat;
  background-size: 900px 900px, 900px 900px, 900px 900px;
  background-attachment: fixed;
  animation: bganimation 30s infinite;
  min-height: 100vh;
  min-height: 100vh;
  max-width: 100vw;

  .light {
    margin-top: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    user-select: none;

    .box {
      width: 10px;
      height: 10px;
      border: 1px solid black;
      margin-top: 3px;
    }

    &--checked {
      .box {
        background-color: black;
      }
    }
  }

  .dark {
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    user-select: none;

    .box {
      width: 10px;
      height: 10px;
      border: 1px solid black;
      margin-top: 3px;
    }

    &--checked {
      .box {
        background-color: black;
      }
    }
  }

  &--dark {
    background: radial-gradient(
        ellipse at center,
        rgba(0, 0, 255, 0.15) 0%,
        rgba(0, 0, 0, 0) 70%
      ),
      radial-gradient(
        ellipse at center,
        rgba(255, 0, 0, 0.15) 0%,
        rgba(0, 0, 0, 0) 70%
      ),
      radial-gradient(
          ellipse at center,
          rgba(0, 255, 0, 0.15) 0%,
          rgba(0, 0, 0, 0) 70%
        )
        #030303;

    animation: bganimation 30s infinite;
    background-repeat: no-repeat, no-repeat, no-repeat;
    background-size: 900px 900px, 900px 900px, 900px 900px;
    background-attachment: fixed;
    animation: bganimation 30s infinite;

    .frame {
      border-color: grey;
      color: rgb(104, 104, 104) !important;
    }

    .box {
      border-color: grey !important;
    }

    .dark--checked {
      .box {
        background-color: rgb(194, 194, 194);
      }
    }

    .light--checked {
      .box {
        background-color: rgb(194, 194, 194);
      }
    }
  }
}

.frame {
  position: absolute;
  width: calc(100% - 100px);
  height: calc(100vh - 100px);
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-sizing: border-box;
  border: 1px solid black;
  color: rgb(100, 100, 100);
  padding: 5% 5% 3% 5%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  @media screen and (max-width: 600px) {
    width: calc(100% - 40px);
    height: calc(100vh - 40px);
    padding: 5% 5% 3% 5%;
  }
}

.name {
  font-size: 3.5em;
  user-select: none;
  font-weight: 200;

  @media screen and (max-width: 600px) {
    font-size: 1.7em;
  }
}

.sub {
  font-weight: 200;
  user-select: none;
  margin-left: 3px;
}

.copy {
  position: absolute;
  bottom: 15px;
  left: 50px;
  font-size: 0.8em;
  font-weight: 600;
  color: grey;
  @media screen and (max-width: 600px) {
    bottom: 1px;
    left: 20px;
  }
}

.desc {
  // width: 130px;
  font-weight: bold;
  font-size: 0.9rem;

  @media screen and (max-width: 600px) {
    font-size: 0.85rem;
    max-width: 75%;
  }
}

.theme-swithcer {
  display: flex;
  position: absolute;
  right: 15px;
  bottom: 5%;
  text-transform: uppercase;
  font-weight: 300;
  font-size: 0.9rem;
  cursor: pointer;
  writing-mode: vertical-rl;
  direction: rtl;
  text-orientation: mixed;
}

.name-container {
  // display: flex;
  // justify-content: space-between;

  .menu {
    list-style: none;
    width: 200px;
    text-align: left;
    padding: 0;
    margin-left: 6px;
    margin-top: 30px;

    li {
      cursor: pointer;
      margin-bottom: 10px;
      font-weight: bold;
      font-size: 0.9rem;
      color: grey;
      transition: 0.3s;

      .dott {
        width: 8px;
        height: 8px;
        border-radius: 50%;
        background-color: rgb(156, 156, 156);
        display: inline-block;
        margin-right: 10px;
      }

      &:hover {
        color: grey;
      }
    }
  }
}

.home {
  &--dark {
    .desc {
      color: rgb(194, 194, 194);
    }

    .name {
      color: rgb(194, 194, 194);
    }

    .sub {
      color: rgb(170, 170, 170);
    }

    .menu {
      li {
        color: rgb(194, 194, 194);
      }
    }

    .theme-swithcer {
      color: rgb(194, 194, 194);
    }
  }
}
</style>
