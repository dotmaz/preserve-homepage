<template>
  <div id="hero">
    <h1 id="hero-title">📄 Preserve<span class="emphasis">.</span>js</h1>
    <h2 id="hero-subtitle">
      Never lose <span class="emphasis underline">form data</span> again
    </h2>
    <div id="color-splitter"></div>
    <h3 id="hero-subsubtitle">Protect your users from:</h3>
    <div class="hero-container">
      <!-- First item -->
      <div class="hero-item">
        <div class="hero-subitem">
          <h3 class="hero-item-title">
            Unintentional page navigation and script redirects
          </h3>
        </div>
        <div class="hero-subitem">
          <div id="dummy-window">
            <div id="dummy-window-navigation">
              <img id="back-arrow" src="./assets/arrow.png" />
              <img id="forward-arrow" src="./assets/arrow.png" />
              <img
                id="dummy-mouse"
                src="./assets/cursor.svg"
                alt="Dummy Mouse Cursor"
              />
            </div>
            <div id="dummy-window-minimize-navigation">
              <div class="minimize-item"></div>
              <div class="minimize-item"></div>
              <div class="minimize-item"></div>
            </div>
            <div id="dummy-window-overlay"></div>
          </div>
        </div>
      </div>
      <!-- Second item -->
      <div class="hero-item">
        <div class="hero-subitem">
          <h3 class="hero-item-title">API errors and network failures</h3>
        </div>
        <div class="hero-subitem" id="dummy-form-container">
          <div id="dummy-form">
            <div class="dummy-form-item"></div>
            <div class="dummy-form-item"></div>
            <div class="dummy-form-item"></div>
            <div class="dummy-form-item"></div>
            <div class="dummy-form-item"></div>
          </div>
          <div id="dummy-loader">
            <div class="dummy-loader-item"></div>
            <div class="dummy-loader-item"></div>
            <div class="dummy-loader-item">
              <h3 id="dummy-cloud-fail">X</h3>
            </div>
          </div>
          <div id="dummy-api-cloud">
            <img id="dummy-cloud-img" src="./assets/cloud.png" />
          </div>
        </div>
      </div>
      <!-- Third item -->
      <div class="hero-item">
        <div class="hero-subitem">
          <h3 class="hero-item-title">Session timeouts and browser crashes</h3>
        </div>
        <div class="hero-subitem">
          <div id="third-item">⏳</div>
        </div>
      </div>
    </div>
  </div>
  <div id="info">
    <div class="info-section">
      <h1 class="info-title">Try it out</h1>
      <h2 class="info-subtitle">
        • Your data will persist through any reloads
      </h2>
      <h2 class="info-subtitle">• Passwords are never tracked</h2>
      <form>
        <p class="form-title">{{ "Example form" }}</p>
        <label for="email">Email</label>
        <input name="email" type="email" />
        <label for="name">Name</label>
        <input name="name" type="text" />
        <label for="password">Password</label>
        <input name="password" type="password" />
      </form>
    </div>
    <div class="info-section">
      <h1 class="info-title">Install in minutes</h1>
      <h1 class="info-title">Save hours of lost work</h1>
      <div class="cdn-section">
        <div class="cdn-controls">
          <p>CDN Snippet</p>
          <CopyButton></CopyButton>
        </div>
        <div class="code-section">
          &lt;<span class="pink">script</span><br />
          <span class="blue">src</span>="<span class="brown"
            >https://cdn.jsdelivr.net/gh/dotmaz/preservejs@latest/preserve.js</span
          >"&gt;
          <br />
          &lt;/<span class="pink">script</span>&gt;
        </div>
        <br /><br />
        <div class="cdn-controls">
          <p>Initialization Instructions</p>
        </div>
        <div class="code-section">
          <span class="pink">const</span> preserve =
          <span class="blue">new</span> <span class="brown">Preserve</span>();
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CopyButton from "./components/CopyButton";
export default {
  name: "App",
  components: {
    CopyButton,
  },
  mounted() {
    setTimeout(() => {
      this.animateMouseToPosition(5, 10, 500);
    }, 500);
    // Initialize preserve
    const preserve = new window.Preserve();
    console.log(preserve);
  },
  methods: {
    animateMouseToPosition(targetX, targetY, time) {
      const mouseElement = document.getElementById("dummy-mouse");
      if (!mouseElement) {
        console.error("Mouse element not found");
        return;
      }

      const startX = mouseElement.offsetLeft;
      const startY = mouseElement.offsetTop;
      const distanceX = targetX - startX;
      const distanceY = targetY - startY;

      const startTime = performance.now();

      const moveMouse = (currentTime) => {
        const elapsedTime = currentTime - startTime;
        const fractionOfDuration = elapsedTime / time;

        if (fractionOfDuration < 1) {
          mouseElement.style.left =
            startX + distanceX * fractionOfDuration + "px";
          mouseElement.style.top =
            startY + distanceY * fractionOfDuration + "px";
          requestAnimationFrame(moveMouse);
        } else {
          mouseElement.style.left = targetX + "px";
          mouseElement.style.top = targetY + "px";
        }
      };

      requestAnimationFrame(moveMouse);
    },
  },
};
</script>

<style lang="scss">
.cdn-section {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin: 40px 0;
}

.cdn-controls {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-bottom: 20px;

  p {
    color: #fff;
    font-weight: bold;
    margin-right: 30px;
  }
}

.code-section {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
  padding: 40px;
  word-break: break-all;

  border-radius: 13px;
  background: rgba(0, 0, 0, 0.3);

  color: #fff;
  font-weight: bold;
  font-family: monospace !important;
  font-size: 16px;
  line-height: 22px;
  width: 100%;

  max-width: 100%;

  * {
    font-family: monospace !important;
  }

  .pink,
  .blue,
  .brown {
    display: contents;
  }

  .pink {
    color: pink;
  }

  .blue {
    color: lightblue;
  }

  .brown {
    color: burlywood;
  }
}

form {
  display: flex;
  flex-direction: column;
  max-width: 100%;
  width: 400px;
  height: 500px;
  margin-top: 50px;
  text-align: left;

  border: 2px solid white;
  border-radius: 7px;
  padding: 15px;
  color: white;
  font-weight: bold;

  background: rgba(255, 255, 255, 0.1);

  .form-title {
    margin-bottom: 20px;
    font-size: 18px;
    font-weight: bold;
    text-decoration: underline;
    text-underline-offset: 6px;
  }

  input {
    margin: 12px 0;
    border: 1px solid #eee;
    background: rgba(0, 0, 0, 0.05);

    height: 30px;
    outline: none;
    padding: 8px;

    color: white;
    font-weight: bold;

    &:focus {
      border: 2px solid white;
    }
  }
}

body {
  margin: 0;
}

#color-splitter {
  background: linear-gradient(
    to left bottom,
    rgba(29, 116, 222, 1) 50%,
    #ffffff 50%
  );
  height: 10vh;
  width: 100vw;
  margin-top: -10px;

  animation: slideDown 0.5s ease-in-out forwards;

  @keyframes slideDown {
    0% {
      margin-top: -20px;
    }
    100% {
      margin-top: -2px;
    }
  }
}

#hero {
  min-height: 100vh;
  max-height: fit-content;
}

@media screen and (max-width: 450px) {
  #app #info {
    padding: 40px 0px !important;
  }
}

@media screen and (max-width: 1200px) {
  #info {
    flex-direction: column !important;
    align-items: center !important;
    padding: 50px !important;

    .info-section {
      width: 100% !important;
      &:first-child {
        margin-bottom: 50px !important;
      }
    }
  }
}

#info {
  min-width: 100vw;
  max-width: 100vw;
  min-height: 100vh;
  max-height: fit-content;

  background-color: #1d74de;

  padding: 50px;

  display: flex;
  flex-direction: row;

  .info-section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 50%;
    max-width: 90vw;
    padding: 0 20px;

    .info-title {
      color: #fff;
      font-weight: 900;
      font-size: 2.5rem;
      font-family: "Montserrat";
      margin: 5px 0;
    }

    .info-subtitle {
      color: #fff;
      font-weight: 900;
      font-size: 1.5rem;
      font-family: "Montserrat";
      margin: 5px 0;
    }
  }
}

.page-break {
  margin: 20px 0;
}

// .emphasis {
//   color: #1d74de;
// }

.underline {
  text-decoration: underline;
  text-underline-offset: 3px;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0px);
  }
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat" !important;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  #hero-title {
    background: #1d74de;
    margin: 0;
    padding: 90px 0 30px 0;
    font-size: 3em;
    color: white;
  }

  #hero-subtitle {
    background: #1d74de;
    margin: 0;
    margin-top: -1px;
    padding: 30px 0;
    font-weight: 900;
    color: white;
    cursor: pointer;

    span {
      transition-duration: 300ms;
      transition-timing-function: ease-out;
    }

    span:hover {
      background: white;
      color: #1d74de;
      padding: 5px;

      transition-duration: 300ms;
      transition-timing-function: ease-out;
    }
  }

  #hero-subsubtitle {
    max-width: 90vw;
    opacity: 0.6;
    font-size: 2em;
    font-style: italic;
    opacity: 0.5;
    color: #666;
    margin: 40px auto 60px auto;

    animation: fadeIn 0.5s ease-out forwards;
  }
  @media screen and (max-width: 900px) {
    .hero-container {
      flex-direction: column !important;
      align-items: center !important;
    }

    .hero-item {
      margin-top: 40px;
      // flex-direction: column-reverse !important;
      // align-items: center;

      .hero-item-title {
        margin-bottom: 50px;
      }
    }
  }

  .hero-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    position: relative;

    .hero-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin: 0 40px 100px 40px;
      position: relative;
      height: fit-content;
      min-width: 100px;
      min-height: 100px;
      // margin: 20%;

      // Pre-animation props
      opacity: 0;
      transform: translateY(50px);

      animation: fadeIn 0.5s ease-out forwards;

      &:nth-child(1) {
        animation-delay: 0.5s;
      }
      &:nth-child(2) {
        animation-delay: 1s;
      }
      &:nth-child(3) {
        animation-delay: 1.5s;
      }

      .hero-item-title {
        max-width: 300px;
        text-align: center;
        margin-bottom: 50px;
      }
    }
  }
}

#dummy-api-cloud {
  position: relative;
  #dummy-cloud-img {
    width: 60px;
    opacity: 0.5;
  }
}

#dummy-cloud-fail {
  font-size: 20px;
  position: absolute;
  margin: 0;
  top: -8.5px;
  left: 0;
  font-weight: 900;
  color: transparent;
  animation: fadeRed 0.3s forwards;
  animation-delay: 2.5s;

  @keyframes fadeRed {
    0% {
      transform: none;
      color: transparent;
    }
    50% {
      transform: rotateZ(30deg);
    }
    100% {
      transform: none;
      color: #e03e38;
    }
  }
}

#dummy-form-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;

  #dummy-loader {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin: 0 15px;

    .dummy-loader-item {
      position: relative;
      background: #ccc;
      width: 10px;
      height: 10px;
      border-radius: 50%;
      margin: 0 8px;

      animation: fadeDark 0.15s linear forwards;

      &:nth-child(1) {
        animation-delay: 1.5s;
      }
      &:nth-child(2) {
        animation-delay: 2s;
      }
      &:nth-child(3) {
        animation: fadeOut 0.05s linear forwards !important;
        animation-delay: 2.5s !important;
      }

      @keyframes fadeDark {
        0% {
          background: #ccc;
        }
        100% {
          background: #666;
        }
      }

      @keyframes fadeOut {
        0% {
          background: #ccc;
        }
        100% {
          background: transparent;
        }
      }
    }
  }
}

#dummy-form {
  width: 70px;
  height: 100px;
  box-shadow: 0 0 10px 0px rgba(0, 0, 0, 0.1);
  border-radius: 7px;
  padding: 10px;

  .dummy-form-item {
    width: 6px;
    height: 6px;
    border-radius: 3px;
    background-color: #ccc;
    margin: 10px 0;

    &:nth-child(1) {
      animation: expandRightSmall 1s 1s ease-out forwards;
    }
    &:nth-child(2) {
      animation: expandRightBig 0.8s 1.25s ease-out forwards;
    }
    &:nth-child(3) {
      animation: expandRightBig 0.6s 1.5s ease-out forwards;
    }
    &:nth-child(4) {
      animation: expandRightSmall 1.2s 1.75s ease-out forwards;
    }
    &:nth-child(5) {
      animation: expandRightBig 1s 2s ease-out forwards;
    }

    @keyframes expandRightSmall {
      100% {
        width: 30px;
      }
    }
    @keyframes expandRightBig {
      100% {
        width: 50px;
      }
    }
  }
}

#dummy-window {
  width: 200px;
  height: 100px;
  box-shadow: 0 0 10px 2px rgba(0, 0, 0, 0.1);
  border-radius: 13px;
  transform: scale(1.2);

  #dummy-mouse {
    position: absolute;
    left: 100px;
    top: 40px;
    width: 30px;
    z-index: 3;

    animation: shrinkAnimation 0.2s 0.5s ease-out forwards;

    @keyframes shrinkAnimation {
      100% {
        transform: scale(0.9);
      }
    }
  }

  #dummy-window-overlay {
    background: red;
    width: calc(100% + 100px);
    height: 100px;
    position: absolute;
    bottom: -40px;
    left: -50px;
    background: linear-gradient(to top, white 50%, transparent);
    z-index: 2;
  }

  #dummy-window-navigation {
    position: absolute;
    top: 5px;
    left: 5px;
    display: flex;

    #back-arrow {
      margin-right: 5px;
      width: 25px;
      opacity: 0.5;
      transform: rotateZ(180deg);
      animation: darken 0.3s 0.5s ease-out forwards;

      @keyframes darken {
        100% {
          opacity: 0.8;
        }
      }
    }

    #forward-arrow {
      opacity: 0.5;
      width: 25px;
    }
  }

  #dummy-window-minimize-navigation {
    position: absolute;
    top: 12px;
    right: 10px;
    display: flex;
    flex-direction: row;

    .minimize-item {
      width: 12px;
      height: 12px;
      opacity: 0.8;
      margin: 0 3px;
      border-radius: 50%;

      &:nth-child(1) {
        background-color: #34c749;
      }
      &:nth-child(2) {
        background-color: #fdbc40;
      }
      &:nth-child(3) {
        background-color: #fc5753;
      }
    }
  }
}

#third-item {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;

  font-size: 50px;

  // Pre-animation props
  transform: rotateZ(0deg);

  animation: rotate 3s ease-in-out infinite;
  @keyframes rotate {
    0% {
      transform: rotateZ(0deg);
    }
    50% {
      transform: rotateZ(180deg);
    }
    100% {
      transform: rotateZ(360deg);
    }
  }
}
</style>
