<template>
  <div class="blog-container" @mousemove="handleMouseMove">
    <!-- 顶部部分 -->
    <div class="BlogTop">
      <h1 class="header-name">Jack Ye</h1>
      <div class="button-container">
        <button class="nav-button" @click="scrollToTop">Home</button>
        <button class="nav-button" @click="scrollTo('Favorite')">Favorite</button>
        <button class="nav-button" @click="scrollTo('Game')">Game</button>
        <button class="nav-button" @click="scrollTo('Books')">Investment</button>
        <button class="nav-button" @click="scrollTo('Music')">Music</button>
        <button class="github-button" @click="goToGitHub"></button>
      </div>
    </div>

    <div class="CardContainer">
      <FloatingDots 
        :quantity="100"
        :ease="80"
        color="#ffffff"
        class="floating-background"
      />
      <!-- 3D 名字卡片 -->
      <div id="name-card" class="name-card" :style="cardStyle">
        <p class="name-label">My name is:</p>
        <div class="name-container" @mouseenter="hover = true" @mouseleave="hover = false">
          <h1 class="first-name" :class="{ fade: isFading, hover: hover }">{{ currentName }}</h1>
        </div>
        <br>
        <!-- 添加白色分隔线 -->
        <hr class="divider2" />
        <!-- WhoAmI 部分 -->
        <div class="WhoAmI">
          <p>I am a:</p>
          <div class="job-list">
            <div class="MyJob" @mouseenter="hoverJob = 'Programer'" @mouseleave="hoverJob = null">
              <p :class="{ hover: hoverJob === 'Programer' }">Programer</p>
            </div>
            <div class="MyJob" @mouseenter="hoverJob = 'Web Developer'" @mouseleave="hoverJob = null">
              <p :class="{ hover: hoverJob === 'Web Developer' }">Web Developer</p>
            </div>
            <div class="MyJob" @mouseenter="hoverJob = 'Game Player'" @mouseleave="hoverJob = null">
              <p :class="{ hover: hoverJob === 'Game Player' }">Game Player</p>
            </div>
            <div class="MyJob" @mouseenter="hoverJob = 'College Student'" @mouseleave="hoverJob = null">
              <p :class="{ hover: hoverJob === 'College Student' }">College Student</p>
            </div>
          </div>
        </div>
        <!-- 图标部分 -->
        
      </div>
    </div>

    <div class="tracks">
          <div class="track1"></div> <!-- 添加轨道 -->
          <div class="track2"></div> <!-- 添加轨道 -->
          <div class="track3"></div> <!-- 添加轨道 -->
    </div>
    <div class="icons">
      <div class="icon google" @mouseenter="stopIconMovement('google')" @mouseleave="startIconMovement('google')" style="transform: rotate(0deg) translate(325px) rotate(0deg);"></div>
      <div class="icon edge" @mouseenter="stopIconMovement('edge')" @mouseleave="startIconMovement('edge')" style="transform: rotate(90deg) translate(325px) rotate(0deg);"></div>
      <div class="icon steam" @mouseenter="stopIconMovement('steam')" @mouseleave="startIconMovement('steam')" style="transform: rotate(180deg) translate(325px) rotate(0deg);"></div>
      <div class="icon ps" @mouseenter="stopIconMovement('ps')" @mouseleave="startIconMovement('ps')" style="transform: rotate(270deg) translate(325px) rotate(0deg);"></div>
    </div>

    <!-- Add Favorite Section -->
    <div id="Favorite" class="Favorite" style="width: 100%; height: 1300px; background-color: #1a1a1a;">
      <h2 class="favorite-title"></h2>
      <div class="favorite-content">
        <!-- First Row -->
        <div class="favorite-row">
          <DirectionAwareHover 
            imageUrl="/img/miyazaki.png"
            alt="miyazaki"
          >
            <h3 class="text-xl font-bold">Hidetaka Miyazaki</h3>
            <p class="text-sm mt-2">Hidetaka Miyazaki is a game designer at FromSoftware. 
              He is the mastermind behind many games, including Elden Ring, Sekiro, and Bloodborne. 
              The epic sense of Elden Ring captivated me so deeply that I couldn't pull myself away while playing.
               He is probably the most creative designer I have ever seen.</p>
          </DirectionAwareHover>

          <DirectionAwareHover 
            imageUrl="/img/ps5.png"
            alt="ps5"
          >
            <h3 class="text-xl font-bold">Playstation 5</h3>
            <p class="text-sm mt-2">The PS5 is currently the platform I use the most for gaming. 
              It offers a wide variety of high-quality games, such as Gran Turismo and The Last of Us. 
              Combined with the controller's refined haptic feedback, it provides an incredibly immersive experience.</p>
          </DirectionAwareHover>

          <DirectionAwareHover 
            imageUrl="/img/jojo.png"
            alt="GitHub"
          >
            <h3 class="text-xl font-bold">JOJO's Bizarre Adventure</h3>
            <p class="text-sm mt-2">JOJO's Bizarre Adventure is a manga series created by Hirohiko Araki. 
              It follows the story of the Joestar family, who are cursed with the power of the JoJo family's spirit. 
              The series is known for its unique and diverse characters, as well as its complex plot and philosophical themes.</p>
          </DirectionAwareHover>
        </div>

        <!-- Second Row -->
        <div class="favorite-row">
          <DirectionAwareHover 
            imageUrl="/img/mj.png"
            alt="Michael Jackson"
          >
            <h3 class="text-xl font-bold">Michael Jackson</h3>
            <p class="text-sm mt-2">Michael Jackson is a legendary singer and dancer. 
              His music and dance moves have inspired countless artists and fans. 
              His unique voice and charismatic performances have left a lasting impact on the music industry.
              I love his songs like Beat It, Thriller, and Dangerous. 
              Overall, every one of his songs is worth listening to.</p>
          </DirectionAwareHover>

          <DirectionAwareHover 
            imageUrl="/img/bitcoin.jpg"
            alt="Bitcoin Logo"
          >
            <h3 class="text-xl font-bold">Btccoin&BlockChain</h3>
            <p class="text-sm mt-2">I have been learning about blockchain technology and cryptocurrencies for a long time. 
              I believe that blockchain technology will be the future of the world, and I am very interested in it.</p>
          </DirectionAwareHover>


        </div>
      </div>
    </div>

    <div class="GBM" style="top: 2400px;">
      <!-- Game Section -->
      <div id="Game" class="Game" style="width: 100%; height: 1600px; background-color: #1a1a1a">
       
        <div class="game-content">
          <div class="pin-wrapper">
            <ThreeDPin title="my-steam" href="https://steamcommunity.com/id/gamerjky/">
              <div class="pin-inner-content2">
                <h3 class="pin-title2">My steam account</h3>
                <div class="pin-description2">
                  <span>You can search my id: <span style="color: yellow;">GamerJKY</span> to add my steam friend if you want to play game on steam with me.</span>
                </div>
                <div class="pin-gradient"></div>
              </div>
            </ThreeDPin>
          </div>
          
          <!-- 新增的第二个pin-wrapper -->
          <div class="pin-wrapper2">
            <ThreeDPin title="my-playstation" href="https://psnine.com/psnid/xh_jky">
              <div class="pin-inner-content2">
                <h3 class="pin-title2">My playstation account</h3>
                <div class="pin-description2">
                  <span>You can search my id: <span style="color: yellow;">xh_jky</span> to add my playstation friend if you want to play game on playstation with me.<br></span>
                </div>
                <div class="pin-gradient2"></div>
              </div>
            </ThreeDPin>
          </div>


          <ThreeDCarousel class="TDC"/>
          <AnimatedTestimonials class="testimonials-section" />
          <div class="infi-background"></div>
          <InfiniteMovingCards class="infinite-cards" speed="slow" />
        </div>

      </div>

      <!-- Investment Section -->
      <div id="Investment" class="Investment" style="width: 100%; height: 800px; background-color: #1a1a1a;">
        <h2>Investment Section</h2>
      </div>
    </div>
  </div>
</template>

<script>
import FloatingDots from './FloatingDots.vue'
import ThreeDCarousel from './ThreeDCarousel.vue'
import AnimatedTestimonials from './AnimatedTestimonials.vue'
import ThreeDPin from './3DPin.vue'
import InfiniteMovingCards from './InfiniteMovingCards.vue'
import DirectionAwareHover from './DirectionAwareHover.vue'

export default {
  name: 'MyBlog',
  components: {
    FloatingDots,
    ThreeDCarousel,
    AnimatedTestimonials,
    ThreeDPin,
    InfiniteMovingCards,
    DirectionAwareHover
  },
  data() {
    return {
      cardStyle: {
        transform: 'perspective(1000px) rotateY(0deg) rotateX(0deg)',
        boxShadow: '0 10px 30px rgba(0, 0, 0, 0.5)',
      },
      names: ['Jack Ye', '叶 学 航'], // 定义名字数组
      currentIndex: 0, // 当前显示的名字索引
      isFading: false, // 控制淡入淡出效果
      hover: false, // 控制悬停状态
      hoverJob: null, // 控制当前悬停的职业
    };
  },
  computed: {
    currentName() {
      return this.names[this.currentIndex]; // 根据索引返回当前名字
    },
  },
  methods: {
    handleMouseMove(event) {
      const card = document.querySelector('.name-card');
      if (!card) return;

      const rect = card.getBoundingClientRect();
      const mouseX = event.clientX - rect.left;
      const mouseY = event.clientY - rect.top;
      
      const rotateX = ((mouseY - rect.height / 2) / rect.height) * -5;
      const rotateY = ((mouseX - rect.width / 2) / rect.width) * 5;

      this.cardStyle = {
        transform: `
          perspective(1000px)
          rotateX(${rotateX}deg)
          rotateY(${rotateY}deg)
          scale3d(1.01, 1.01, 1.01)
        `,
        transition: 'transform 0.2s ease-out',
      };
    },
    handleMouseLeave() {
      this.cardStyle = {
        transform: 'perspective(1000px) rotateX(0deg) rotateY(0deg) scale3d(1, 1, 1)',
        transition: 'transform 0.3s ease-out',
      };
    },
    switchName() {
      this.isFading = true; // 开始淡出
      setTimeout(() => {
        this.currentIndex = (this.currentIndex + 1) % this.names.length; // 切换名字索引
        this.isFading = false; // 开始淡入
      }, 500); // 500ms后切换名字
    },
    scrollTo(section) {
      const element = document.getElementById(section);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' }); // 平滑滚动到目标元素
      }
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' }); // 平滑滚动到页面顶部
    },
    goToGitHub() {
      window.location.href = 'https://github.com/JustaNewer'; // 跳转到 GitHub
    },
    goToSteam(){
      window.location.href = 'https://steamcommunity.com/id/gamerjky/';
    },
  },
  mounted() {
    setInterval(this.switchName, 2000); // 每两秒切换名字
  },
};
</script>

<style scoped>
.blog-container {
  width: 100%; /* 设置宽度为100% */
  height: 100%; /* 设置高度为100% */
  margin: 0;
  padding: 0;
  background-color: #1a1a1a;
  color: #ffffff;
  display: flex;
  flex-direction: column; /* 垂直排列 */
}

.BlogTop {
  width: 90%;
  position: fixed;
  top: 15px;
  left: 50%;
  transform: translateX(-50%);
  background-color: rgba(0, 0, 0, 0.5);
  padding: 20px;
  z-index: 20;
  display: flex;
  align-items: center;
  border-radius: 50px 50px 50px 50px;
  margin: 0 auto;
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
}

.header-name {
  font-size: 2em;
  color: #ffffff;
  margin: 0 20px 0 0; /* 右边距 */
}

.button-container {
  display: flex;
  gap: 30px; /* 按钮之间的间距 */
  padding: 10px; /* 按钮的内边距 */
}

.nav-button {
  background-color: #3d3d3d; /* 按钮背景色 */
  color: #ffffff; /* 按钮文字颜色 */
  border: none; /* 去掉边框 */
  border-radius: 20px; /* 圆角矩形 */
  padding: 10px 20px; /* 按钮内边距 */
  cursor: pointer; /* 鼠标悬时显示手型 */
  transition: background-color 0.3s ease, transform 0.2s ease; /* 添加动画效果 */
}

.nav-button:hover {
  background-color: #5d5d5d; /* 悬停时的背景色 */
  transform: scale(1.05); /* 悬停时放大 */
}

.nav-button:active {
  transform: scale(0.95); /* 点击时缩小 */
}


.name-card {
  background: rgba(45, 45, 45, 0.98);
  border-radius: 20px;
  padding: 40px;
  text-align: center;
  position: absolute;
  top: 200px;
  left: calc(50% - 225px);
  width: 450px;
  height: 450px;
  transform-style: preserve-3d;
  transition: all 0.3s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
  z-index: 10;
  position: relative;
}

.name-label {
  transform: translateZ(20px);
  position: absolute;
  top: 30px;
  left: 30px;
  font-size: 1.2em;
  color: rgba(255, 255, 255, 0.8);
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.name-card:hover .name-label {
  transform: translateZ(50px);
}

.name-container {
  position: absolute;
  left: 150px;
  top: 70px;
  width: 170px;
  height: 65px;
  transform: translateZ(30px);
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.name-card:hover .name-container:hover {
  transform: translateZ(80px);
}

.first-name {
  transform: translateZ(40px);
  transition: all 0.3s ease;
}

.first-name {
  font-size: 2.5em; /* 字体大小，调整为较小的值 */
  color: orange; /* 字体颜色改为色 */
  margin: 0 5px; /* 控制两个名字之间的间距 */
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  transition: opacity 0.5s ease, box-shadow 0.3s ease; /* 添加淡入淡出效果和阴影效果 */
}

.first-name:hover {
  text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.5); /* 悬浮时添加阴影效果 */
}

.fade {
  opacity: 0; /* 淡出效果 */
}

/* 鼠标悬停时的效果 */
.name-container:hover {
  transform: translateY(-20px) scale(1.05); /* 向上移动20px并放大 */
}

/* 新增的分隔线样式 */
.divider2 {
  transform: translateZ(20px);
  width: 85%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  position: absolute;
  top: 130px;
  left: 30px;
}

.name-card:hover .divider2 {
  transform: translateZ(40px);
  background: linear-gradient(90deg, transparent, rgba(255, 165, 0, 0.3), transparent);
}

/* WhoAmI 样式 */
.WhoAmI {
  transform: translateZ(30px);
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.name-card:hover .WhoAmI {
  transform: translateZ(60px);
}

.WhoAmI p {
  transform: translateZ(35px);
  transition: transform 0.3s ease;
}

.WhoAmI {
  width: 90%; /* 设置宽度与卡片一致 */
  height: 65%; /* 高度为卡片的剩余高度 */
  text-align: center; /* 文本居中 */
  color: #ffffff; /* 字体颜色 */
  margin-top: 10px; /* 与divider2的间距 */
  position: absolute; /* 绝对定位 */
  bottom: 0; /* 靠近卡片底部 */
}

.WhoAmI p {
  position: absolute; /* 绝对定位 */
  top: 10px; /* 距离上边距10px */
  left: 10px; /* 距离左边距10px */
  margin: 0; /* 去掉默认的margin */
  font-size: 1.2em; /* 字体大小 */
}

.job-list {
  display: flex;
  flex-direction: column; /* 垂直排列职业 */
  align-items: center; /* 水平居中对齐 */
  transform-style: preserve-3d;
}

.MyJob {
  transform: translateZ(40px);
  transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  width: 200px;
  height: 50px; /* 调整高度以适应内容 */
  margin: 10px 0; /* 添加上下间距 */
  position: relative; /* 相对定位 */
  margin-left: 50px; /* 向右移动50px */
  background: transparent; /* 设置背景为透明 */
  perspective: 500px; /* 添加透视效果 */
}

.name-card:hover .MyJob {
  transform: translateZ(70px);
}

/* 悬浮效果 */
.MyJob p {
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  padding: 10px 20px;
  border-radius: 8px;
}

.name-card:hover .MyJob:hover p {
  transform: translateZ(100px);
  background:transparent;
  

}

.GBM{
  width: 100%;
  top: 2400px;
  position: absolute;
}

.icons {
  position: absolute; /* 绝对定位 */
  top: 200px; /* 距离卡片顶部20px */
  left: 50%; /* 水平居中 */
  transform: translateX(-50%); /* 使其真正居中 */
  z-index: 1;
  gap: 0; /* 图标之间的间距 */
  width: 58px;
  height: 58px;
  z-index: 1;
}

.icon {
  width: 50px; /* 图标宽度 */
  height: 50px; /* 图标高度 */
  border-radius: 50%; /* 圆形图标 */
  background-size: cover; /* 背景图像覆盖 */
  top: 100px;
  animation: rotate 10s linear infinite;
  position: relative;
  
}

.google {
  width: 90px; 
  height: 90px;
  background-image: url('/img/google.png'); /* Google 图标 */
  animation: rotateGoogle 5s linear infinite; /* 顺时针运动 */
  animation-duration: 5s;

}

.edge {
  background-image: url('/img/github.png'); /* Edge 图标 */
  animation: rotateEdge 6s linear infinite; /* 顺时针运动 */
  animation-duration: 6s;

}

.steam {
  background-image: url('/img/steam.png'); /* Steam 图标 */
  animation: rotateSteam 7s linear infinite; /* 顺时针运动 */
  animation-duration: 7s;

  width: 70px; /* 图标宽度 */
  height: 70px;
}

.ps {
  background-image: url('/img/ps.png'); /* PS 图标 */
  animation: rotatePS 8s linear infinite; /* 顺时针运动 */
  animation-duration: 8s;

}

.CardContainer{
  perspective: 1000px;
  transform-style: preserve-3d;
  width: 100%;
  height: 800px;
  position: relative;
  z-index: 10;
  overflow: hidden;  /* 添加此行以确保点不会溢出 */
}
.track1 {
  position: absolute;
  width: 600px; /* 直径为500px */
  height: 600px; /* 直径为500px */
  border: 2px dashed  #2D2D2D; /* 白色虚线 */
  border-radius: 50%; /* 圆形 */
  top :200px; /* 垂直居中 */
  left: 50%; /* 水平居中 */
  transform: translate(-50%, -50%); /* 使其真正居中 */
  z-index: -1;
}

.track2 {
  position: absolute;
  width: 675px; /* 直径为500px */
  height: 675px; /* 直径为500px */
  border: 2px dashed rgb(171, 171, 171); /* 白色虚线 */
  border-radius: 50%; /* 圆形 */
  top :200px; /* 垂直居中 */
  left: 50%; /* 水平居中 */
  transform: translate(-50%, -50%); /* 使其真正居中 */
  z-index: -2;
}
.track3 {
  position: absolute;
  width: 750px; /* 直径为500px */
  height: 750px; /* 直径为500px */
  border: 2px dashed white; /* 白色虚线 */
  border-radius: 50%; /* 圆形 */
  top :200px; /* 垂直居中 */
  left: 50%; /* 水平居中 */
  transform: translate(-50%, -50%); /* 使其真正居中 */
  z-index: -3;
}

/* 修改 tracks 容器的样式 */
.tracks {
  position: absolute;
  width: 750px;
  height: 750px;
  top: 425px; /* 与 name-card 的 top 值保持一致 */
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 0;
}

/* 修改轨道样式，使其相对于 tracks 容器定位 */
.track1, .track2, .track3 {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.track1 {
  width: 600px;
  height: 600px;
  border: 2px dashed #2D2D2D;
  z-index: 1;
}

.track2 {
  width: 675px;
  height: 675px;
  border: 2px dashed rgb(171, 171, 171);
  z-index: 2;
}

.track3 {
  width: 750px;
  height: 750px;
  border: 2px dashed white;
  z-index: 3;
}

.github-button{
  background-image: url('/img/github.png');
  background-size: contain;
  border-radius: 50px;
  border: none;
  width: 60px;
  height: 60px;
  position: absolute;
  top: 20px;
  right: 30px;
  cursor: pointer;
  transition: transform 0.3s ease;
}

/* 鼠标悬停时的效果 */
.github-button:hover {
  transform: scale(1.1); /* 悬停时略微放大 */
}

/* 鼠标点击时的效果 */
.github-button:active {
  transform: scale(0.95); /* 点击时缩小 */
}

/* 动画定义 */
@keyframes rotateGoogle {
  0% {
    transform: rotate(0deg) translate(325px) rotate(0deg); /* 325px 为半径 */
  }
  100% {
    transform: rotate(360deg) translate(325px) rotate(0deg);
  }
}

@keyframes rotateEdge {
  0% {
    transform: rotate(0deg) translate(325px) rotate(0deg); /* 325px 为半径 */
  }
  100% {
    transform: rotate(360deg) translate(325px) rotate(0deg);
  }
}

@keyframes rotateSteam {
  0% {
    transform: rotate(0deg) translate(325px) rotate(0deg); /* 325px 为半径 */
  }
  100% {
    transform: rotate(360deg) translate(325px) rotate(0deg);
  }
}

@keyframes rotatePS {
  0% {
    transform: rotate(0deg) translate(325px) rotate(0deg); /* 325px 为半 */
  }
  100% {
    transform: rotate(360deg) translate(325px) rotate(0deg);
  }
}

.floating-background {
  z-index: 2;
}

/* 确保 name-card 在浮点之上 */
.name-card {
  z-index: 2;
  /* ... 其他样式保持不变 ... */
}

.Game {
  padding: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 30px;
  background-image: url('/img/psSymbol.jpg');
  background-repeat: repeat; /* 图片重复 */
  background-size: 100px; /* 控制重复图片的大小 */
  position: relative; /* 为遮罩层提供定位上下文 */
  top: -300px;
}

/* 添加一个半透明遮罩层，使背景不会影响内容的可读性 */
.Game::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(26, 26, 26, 0.9); /* 与原背景色相同，但带透明度 */
  z-index: 1;
}

/* 确保内容在遮罩层之上 */
.Game h2, 
.Game h3, 
.Game > * {
  position: relative;
  z-index: 2;
}

.Game h2 {
  font-size: 2.5em;
  color: #ffffff;
  margin-bottom: 20px;
}

.game-content {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 50px; /* 控制轮播图和testimonials之间的距离 */
}








.testimonials-section {
  position: absolute;
  left: -40px;
  top: 500px;
  width:70%;
  height: 390px;
  background-color: rgba(255, 165, 0,0.5); /* 半透明橙色 */
  border-radius: 20px;
  z-index: 2; /* 确保内容在背景之上 */
}



.TDC{
  position: absolute;
  top: 70px;
  right: 0px;
  width: 65%;
  height: 390px;
  background-color: rgba(82, 146, 255,0.5);
  border-radius: 20px;
}



.pin-wrapper {
  position: absolute;
  width: 25%;
  height: 390px;
  top: 70px;
  left: 5px;
  z-index: 2;
}

.pin-inner-content {
  display: flex;
  flex-direction: column;
  height: 100%;
  color: rgba(255, 255, 255, 0.5);
}

.pin-gradient {
  flex: 1;
  width: 100%;
  margin-top: 16px;
  border-radius: 8px;
  background-image: url('/img/steamacc.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  aspect-ratio: 16/9; /* 或根据您的图片实际比例调整 */
}

.pin-gradient2{
  flex: 1;
  width: 100%;
  margin-top: 16px;
  border-radius: 8px;
  background-image: url('/img/psacc.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  aspect-ratio: 16/9; /* 或根据您的图片实际比例调整 */
}

.pin-wrapper2 {
  position: absolute;
  width: 25%;
  height: 390px;
  top: 550px;
  right: 5px;
  z-index: 2;
}

.infinite-cards {
  position: absolute;
  top: 1100px;
  z-index: 2;
}

.infi-background {
  position: absolute;
  width: 100%;
  height: 390px;
  top: 1000px;
  background-color: rgb(37, 88, 45);
  border-radius: 20px;
}

.divider {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  margin: 0;
  border: none;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.3),
    transparent
  );
}

.Favorite {
  padding: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  top: 800px;
  background-image: url('/img/bgwb.jpg');
  background-repeat: repeat;
  background-size: auto;
  width: 100%;
}

.favorite-title {
  font-size: 2.5em;
  color: #ffffff;
  margin-bottom: 60px;
  text-align: center;
}

.favorite-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  gap: 100px;
  padding: 2rem;
}

.text-xl {
  font-size: 1.25rem;
  line-height: 1.75rem;
}

.text-sm {
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.font-bold {
  font-weight: 700;
}

.mt-2 {
  margin-top: 0.5rem;
}

.favorite-row {
  display: flex;
  justify-content: center;
  gap: 60px;
  width: 100%;
}
.Investment{
  position: absolute; 
  top: 1200px;
}
</style>
