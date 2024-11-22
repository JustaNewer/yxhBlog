<template>
    <div class="blog-container">
      <!-- 头部区域 -->
      <header class="header">
        <h1>Jack Ye</h1>
        <p class="subtitle">Personal Blog & Portfolio</p>
      </header>
  
      <!-- 导航栏 -->
      <nav class="navigation">
        <ul>
          <li><a href="#home">Home</a></li>
          <li><a href="#about">About</a></li>
          <li><a href="#blog">Blog</a></li>
          <li><a href="#projects">Projects</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>
      </nav>
  
      <!-- 主要内容区域 -->
      <main class="main-content">
        <!-- 最新博客文章 -->
        <section class="latest-posts">
          <h2>Latest Posts</h2>
          <div class="posts-grid">
            <article class="post-card" v-for="post in posts" :key="post.id">
              <img :src="post.image" :alt="post.title">
              <div class="post-content">
                <h3>{{ post.title }}</h3>
                <p>{{ post.excerpt }}</p>
                <span class="date">{{ post.date }}</span>
              </div>
            </article>
          </div>
        </section>
      </main>
  
      <!-- 页脚 -->
      <footer class="footer">
        <p>&copy; 2024 Jack Ye. All rights reserved.</p>
        <div class="social-links">
          <a href="#"><i class="fab fa-github"></i></a>
          <a href="#"><i class="fab fa-linkedin"></i></a>
          <a href="#"><i class="fab fa-twitter"></i></a>
        </div>
      </footer>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MyBlog',
    data() {
      return {
        posts: [
          {
            id: 1,
            title: 'Getting Started with Vue.js',
            excerpt: 'Learn the basics of Vue.js and how to build your first application.',
            image: '/images/vue-post.jpg',
            date: 'March 15, 2024'
          },
          // 可以添加更多文章
        ]
      }
    }
  }
  </script>
  
  <style scoped>
  .blog-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .header {
    text-align: center;
    padding: 50px 0;
    background: #f8f9fa;
    border-radius: 8px;
    margin-bottom: 30px;
  }
  
  .header h1 {
    font-size: 3em;
    color: #2c3e50;
    margin-bottom: 10px;
  }
  
  .subtitle {
    font-size: 1.2em;
    color: #666;
  }
  
  .navigation {
    margin-bottom: 40px;
  }
  
  .navigation ul {
    list-style: none;
    padding: 0;
    display: flex;
    justify-content: center;
    gap: 30px;
  }
  
  .navigation a {
    text-decoration: none;
    color: #2c3e50;
    font-weight: 500;
    font-size: 1.1em;
    transition: color 0.3s;
  }
  
  .navigation a:hover {
    color: #42b883;
  }
  
  .latest-posts {
    margin-bottom: 50px;
  }
  
  .posts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    padding: 20px 0;
  }
  
  .post-card {
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 15px rgba(0,0,0,0.1);
    transition: transform 0.3s;
  }
  
  .post-card:hover {
    transform: translateY(-5px);
  }
  
  .post-card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }
  
  .post-content {
    padding: 20px;
  }
  
  .post-content h3 {
    margin: 0 0 10px 0;
    color: #2c3e50;
  }
  
  .date {
    color: #666;
    font-size: 0.9em;
  }
  
  .footer {
    text-align: center;
    padding: 30px 0;
    margin-top: 50px;
    border-top: 1px solid #eee;
  }
  
  .social-links {
    margin-top: 20px;
  }
  
  .social-links a {
    margin: 0 10px;
    color: #2c3e50;
    font-size: 1.5em;
    transition: color 0.3s;
  }
  
  .social-links a:hover {
    color: #42b883;
  }
  </style>