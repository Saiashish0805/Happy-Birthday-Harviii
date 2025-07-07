<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>StoryGems - Monthly Book Surprise!</title>
  <style>
    /* === LOGIN SCREEN === */
    #login-screen {
      position: fixed;
      inset: 0;
      background: #000;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 9999;
    }
    .login-box {
      background: cyan;
      padding: 2.5rem;
      border-radius: 25px;
      box-shadow: 0 0 30px 10px cyan;
      text-align: center;
      max-width: 400px;
      width: 90%;
    }
    .login-box h2 {
      margin-bottom: 1.5rem;
      color: #000;
      font-weight: bold;
    }
    .login-box input {
      display: block;
      width: 100%;
      padding: 0.7rem;
      margin: 0.6rem 0;
      border-radius: 20px;
      border: none;
      font-size: 1rem;
      text-align: center;
    }
    .login-box a {
      display: block;
      margin-top: 0.5rem;
      font-size: 0.9rem;
      color: #333;
      text-decoration: underline;
      cursor: pointer;
    }
    .login-box button {
      margin-top: 1rem;
      background: #000;
      color: cyan;
      font-weight: bold;
      padding: 0.7rem 1.5rem;
      border: none;
      border-radius: 20px;
      cursor: pointer;
      font-size: 1rem;
    }
    .login-box button:hover {
      background: #111;
    }
    .login-box .socials {
      display: flex;
      justify-content: center;
      gap: 1.5rem;
      margin-top: 1.5rem;
    }
    .login-box .socials div {
      text-align: center;
      font-size: 0.85rem;
    }
    .login-box .socials img {
      width: 32px;
      height: 32px;
      margin-bottom: 0.3rem;
    }

    /* === HIDE MAIN UNTIL LOGIN === */
    body.logged-out #main-content {
      display: none;
    }

    /* ============ GLOBAL STYLES ============ */
    body{
      font-family:'Segoe UI',sans-serif;margin:0;padding:0;
      background:#f4f4f9;color:#333;line-height:1.6;
    }
    header{
      background:#6c5ce7;padding:1rem 3rem;position:sticky;top:0;z-index:1000;
      box-shadow:0 4px 8px rgba(0,0,0,.1);
    }
    .header-content{display:flex;justify-content:space-between;align-items:center;gap:1.5rem;flex-wrap:wrap;}
    header h1{color:#fff;font-size:2rem;margin:0;}
    nav a{margin:0 15px;color:#fff;text-decoration:none;font-weight:bold;font-size:1.1rem;position:relative;cursor:pointer;}
    nav a:hover{color:#ffeaa7;}
    nav a::after{content:'';position:absolute;bottom:-5px;left:0;width:100%;height:2px;background:#ffeaa7;transform:scaleX(0);transition:transform .3s;transform-origin:bottom right;}
    nav a:hover::after{transform:scaleX(1);transform-origin:bottom left;}

    /* ============ SEARCH BAR ============ */
    .search-bar input{
      padding:.55rem 1.1rem;border-radius:25px;border:1px solid #ddd;font-size:1rem;
      min-width:200px;outline:none;
    }
    .search-bar input:focus{box-shadow:0 0 0 2px rgba(255,234,167,.8);}
    @media(max-width:600px){ .search-bar input{width:140px;font-size:.85rem;} }

    /* ============ HERO ============ */
    .hero{
      text-align:center;padding:6rem 2rem;color:#fff;
      background-image:linear-gradient(rgba(0,0,0,.55),rgba(0,0,0,.55)),url('https://images.unsplash.com/photo-1512820790803-83ca734da794?auto=format&fit=crop&w=1950&q=80');
      background-size:cover;background-position:center;background-attachment:fixed;
    }
    @media(max-width:768px){.hero{padding:4rem 1.5rem;background-attachment:scroll;}}
    .hero h2{font-size:3rem;margin-bottom:1rem;}
    .hero p{font-size:1.2rem;margin-bottom:2rem;}
    .btn{background:#6c5ce7;color:#fff;padding:.8rem 1.5rem;border:none;border-radius:25px;font-size:1rem;cursor:pointer;text-decoration:none;}
    .btn:hover{background:#ffeaa7;color:#6c5ce7;}

    section{padding:4rem 2rem;text-align:center;}

    /* ============ PLANS & CONTACT ============ */
    .plans,.contact{background:#dff9fb;border-radius:15px;padding:2rem;}
    .plan-option{background:#fff;margin:1rem auto;max-width:400px;padding:1.5rem;border-radius:10px;box-shadow:0 4px 8px rgba(0,0,0,.1);}
    .plan-option:hover{transform:translateY(-5px);transition:.3s;}
    .contact form{max-width:500px;margin:0 auto;}
    .contact input,.contact textarea{width:100%;padding:.8rem;margin:.5rem 0;border-radius:10px;border:1px solid #ccc;}
    .contact button{background:#6c5ce7;color:#fff;padding:.8rem 1.5rem;border:none;border-radius:25px;font-size:1rem;cursor:pointer;}
    .contact button:hover{background:#ffeaa7;}

    /* ============ CATEGORY & TOPIC ============ */
    .book-screen,.topics-screen,.books-list-screen{display:none;padding:4rem 2rem;background:#fff;text-align:center;}
    .category{background:#fff;margin:1rem auto;padding:2rem;max-width:600px;border-radius:10px;box-shadow:0 4px 8px rgba(0,0,0,.1);cursor:pointer;text-align:left;}
    .category:hover{transform:scale(1.05);transition:.3s;}
    .topic-btn{display:inline-block;margin:.7rem 1rem;padding:1rem 1.5rem;background:#6c5ce7;color:#fff;border-radius:25px;font-size:1.2rem;cursor:pointer;}
    .topic-btn:hover{background:#ffeaa7;color:#6c5ce7;}

    /* ============ AMAZON‑STYLE BOOK LIST ============ */
    .book-list{
      display:flex;flex-direction:column;gap:22px;max-width:900px;margin:0 auto;
      padding:0;list-style:none;
    }
    .book-card{
      display:flex;gap:18px;background:#fff;border:1px solid #d8d8d8;border-radius:4px;
      padding:16px;box-shadow:0 2px 6px rgba(0,0,0,.06);cursor:pointer;
    }
    .book-card img{width:90px;height:135px;object-fit:cover;border:1px solid #ccc;}
    .book-info{display:flex;flex-direction:column;justify-content:center;}
    .book-info h4{font-size:1rem;font-weight:600;margin:0;color:#111;}
    .book-info .small-price{margin-top:4px;font-size:.95rem;font-weight:600;color:#b12704;}

    .back-btn{margin-top:2rem;display:inline-block;background:#6c5ce7;color:#fff;padding:.7rem 1.5rem;border-radius:25px;text-decoration:none;cursor:pointer;}
    .back-btn:hover{background:#ffeaa7;color:#6c5ce7;}

    /* ============ DETAIL VIEW ============ */
    .book-detail-wrapper{
      display:flex;gap:30px;flex-wrap:wrap;border:1px solid #d8d8d8;
      padding:20px;border-radius:6px;box-shadow:0 3px 8px rgba(0,0,0,.08);
      max-width:1000px;margin-inline:auto;
    }
    .book-detail-wrapper img{width:180px;height:270px;object-fit:cover;border:1px solid #ccc;}
    .book-detail-info h3{margin:0 0 10px;font-size:1.3rem;}
    .book-detail-info p{margin:6px 0;}
    .price-tag{font-size:1.4rem;font-weight:700;color:#b12704;margin:10px 0;}
    .action-btn{
      background:#ffd814;color:#111;padding:.7rem 1.5rem;border:none;border-radius:8px;
      font-weight:600;cursor:pointer;margin-right:10px;
    }
    .action-btn:hover{background:#f7ca00;}
  </style>
</head>
<body class="logged-out">

  <!-- 🔐 LOGIN SCREEN -->
  <div id="login-screen">
    <div class="login-box">
      <h2>Please Sign in to continue</h2>
      <input type="text" id="username" placeholder="Username" />
      <input type="password" id="password" placeholder="Password" />
      <a onclick="alert('Password recovery coming soon!')">Forgot Password?</a>
      <button onclick="handleLogin()">Sign in or Login</button>
      <a onclick="continueAsGuest()" style="margin-top: 0.8rem; font-size: 0.9rem;">Continue as Guest</a>
      <div class="socials">
        <div>
          <img src="https://img.icons8.com/color/48/000000/google-logo.png" />
          <div>Goo</div>
        </div>
        <div>
          <img src="https://img.icons8.com/color/48/000000/facebook-new.png" />
          <div>Fb</div>
        </div>
        <div>
          <img src="https://img.icons8.com/color/48/000000/phone.png" />
          <div>Pho</div>
        </div>
      </div>
    </div>
  </div>

  <!-- MAIN SITE CONTENT -->
  <div id="main-content">

    <header>
      <div class="header-content">
        <h1>StoryGems💎</h1>
        <nav>
          <a onclick="showHome()">Home</a>
          <a onclick="showBooks()">Books</a>
          <a href="#plans">Plans</a>
          <a href="#contact">Contact</a>
        </nav>
        <!-- Search Bar -->
        <div class="search-bar">
          <input type="search" id="search-input" placeholder="Search books…" oninput="handleSearch(event)" />
        </div>
      </div>
    </header>

    <!-- HOME -->
    <div id="home-screen">
      <section class="hero">
        <h2>Your Monthly Book Adventure Awaits!</h2>
        <p>Get a new book, a bookmark, a mug, and a surprise gift delivered to your door every month!</p>
        <a href="#plans" class="btn">Subscribe Now</a>
      </section>

      <section id="plans" class="plans">
        <h2>📦 Subscription Plans</h2>
        <div class="plan-option"><h3>1 Month</h3><p>1 Book + Bookmark + Mug + Surprise Gift</p></div>
        <div class="plan-option"><h3>2 Months</h3><p>1 Book + Bookmark + Mug + Surprise Gift</p></div>
        <div class="plan-option"><h3>3 Months</h3><p>1 Book + Bookmark + Mug + Surprise Gift</p></div>
      </section>

      <section id="contact" class="contact">
        <h2>📞 Contact Us Jai Balayya</h2>
        <form onsubmit="handleContactForm(event)">
          <input type="text" placeholder="Your Name" required />
          <input type="email" placeholder="Your Email" required />
          <textarea rows="4" placeholder="Your Message" required></textarea>
          <button type="submit">Send</button>
        </form>
      </section>
    </div>

    <!-- CATEGORY -->
    <div id="book-screen" class="book-screen">
      <h2>📚 Explore Our Book Categories</h2>
      <div class="category" onclick="showTopics('kids')"><h3>Kids Books</h3><p>Stories and adventures for young readers!</p></div>
      <div class="category" onclick="showTopics('teens')"><h3>Teens Books</h3><p>Exciting tales for teenage readers!</p></div>
      <div class="category" onclick="showTopics('adults')"><h3>Adults Books</h3><p>Engaging novels and stories for grown‑ups!</p></div>
      <button class="back-btn" onclick="showHome()">Back to Home</button>
    </div>

    <!-- TOPICS -->
    <div id="topics-screen" class="topics-screen">
      <h2>Select a Topic</h2>
      <div id="topics-container"></div>
      <button class="back-btn" onclick="showBooks()">Back to Categories</button>
    </div>

    <!-- BOOKS LIST -->
    <div id="books-list-screen" class="books-list-screen">
      <h2 id="list-heading">Books List</h2>
      <!-- Search results will also render here -->
      <div class="book-list" id="books-list"></div>
      <button class="back-btn" id="list-back-btn" onclick="showTopics(currentCategory)">Back</button>
    </div>

    <!-- BOOK DETAIL -->
    <div id="book-detail-screen" style="display:none;padding:4rem 2rem;background:#fff;">
      <button class="back-btn" onclick="backToList()">← Back to List</button>
      <div id="book-detail" style="margin-top:2rem;"></div>
    </div>

  </div>

  <script>
    /* ---------- DATA ---------- */
    let currentCategory='', currentTopic='';

    /* Topics */
    const topicsData = {
      kids:[
        "Hindu Mythology & Epics",
        "Panchatantra",
        "Hitopadesh & Jataka Tales",
        "Arabian Nights & Islamic Tales",
        "Animal Stories",
        "Fairy Tales & Fables",
        "Science & Discovery"
      ],
      teens:[
        "Fantasy & Adventure","Mystery & Thriller","Romance","Science Fiction",
        "Historical Fiction","Poetry & Drama","Self Help & Motivation"
      ],
      adults:[
        "Literary Fiction","Biography & Memoir","Business & Economics",
        "Health & Wellness","Philosophy & Spirituality","Science & Technology","Politics & Society"
      ]
    };

    /* ---------- Book arrays ---------- */
    const mythBooks = [
      { title: "Krishna: The Cowherd God Hardcover", price: 499, 
       image: "images/1.jpg",
       desc: "The naughtiest kid ever—Krishna who, despite his mischiefs is loved and worshipped by all. A divine child in human form, he is one of the ten incarnations of Lord Vishnu. Besides restoring dharma, he fights demons, tends to cows, is friends with the shepherds, plays flute, and does whatnot. Krishna—The Cowherd God is a beautifully illustrated book to introduce your little ones to the mesmerizing stories of Krishna. Rich in wisdom and knowledge from the Indian mythology, this book is a must-have in your child’s library.A timeless treasury of stories for children!Vibrant and captivating illustrations expand imagination Introduces kids to epic tales and culture of India Simple language makes the stories easy to understand Encourages kids to read Builds a robust vocabulary" },
        { title: "365 Tales of Ganesh", price: 559, image: "images/3.1.jpg",
     desc: "Description coming soon..." },

        { title: "365 Tales of Hanuman", price: 699, image: "images/4.jpg", 
         desc: "Description coming soon..." },
        { title: "365 Krishna Stories: Lord Krishna’s Miracles, Wisdom & Devotion", price: 699, image: "images/5.jpg", 
         desc: "Description coming soon..." },
        { title: "My First Mythology Tale (Illustrated) (Set of 5 Books)", price: 399, image: "images/6.jpg",
         desc: "Description coming soon..." },
        { title: "108 Indian Mythology Stories (Illustrated)", price: 399, image: "images/7.jpg", 
         desc: "Description coming soon..." },
        { title: "Story Book: Krishna The Adorable God (Large Print)", price: 499, image: "images/8.jpg", 
         desc: "Description coming soon..." },
        { title: "My First Shaped Board Book: Goddess Durga", price: 399, image: "images/9.jpg",
         desc: "Description coming soon..." },
        { title: "My First Shaped Board Book: Lord Ganesha", price: 399, image: "images/9.jpg",
         desc: "Description coming soon..." },
        { title: "Mythology Books for Kids (Set of 10 Books)", price: 399, image: "images/10.jpg", 
         desc: "Description coming soon..." },
        { title: "Tales from Indian Mythology [Collection of 10 Books]", price: 619, image: "images/11.jpg" ,
         desc: "Description coming soon..." },
        { title: "365 Stories from the Vedas The Upanishads and the Puranas", price: 650, image: "images/2.jpg", 
         desc: "Description coming soon..." },
        { title: "My First Shaped Board Book: Kali", price: 399, image: "images/9.jpg",
         desc: "Description coming soon..." }
    ];

    /* ---------- DOM ELEMENTS ---------- */
    const loginScreen = document.getElementById('login-screen');
    const mainContent = document.getElementById('main-content');
    const topicsContainer = document.getElementById('topics-container');
    const booksListScreen = document.getElementById('books-list-screen');
    const booksListEl = document.getElementById('books-list');
    const listHeading = document.getElementById('list-heading');
    const listBackBtn = document.getElementById('list-back-btn');
    const bookDetailScreen = document.getElementById('book-detail-screen');
    const bookDetailEl = document.getElementById('book-detail');

    /* ---------- SHOW/HIDE SECTIONS ---------- */
    function showHome() {
      document.getElementById('home-screen').style.display = 'block';
      document.getElementById('book-screen').style.display = 'none';
      document.getElementById('topics-screen').style.display = 'none';
      booksListScreen.style.display = 'none';
      bookDetailScreen.style.display = 'none';
    }

    function showBooks() {
      document.getElementById('home-screen').style.display = 'none';
      document.getElementById('book-screen').style.display = 'block';
      document.getElementById('topics-screen').style.display = 'none';
      booksListScreen.style.display = 'none';
      bookDetailScreen.style.display = 'none';
    }

    function showTopics(category) {
      currentCategory = category;
      currentTopic = '';
      document.getElementById('home-screen').style.display = 'none';
      document.getElementById('book-screen').style.display = 'none';
      document.getElementById('topics-screen').style.display = 'block';
      booksListScreen.style.display = 'none';
      bookDetailScreen.style.display = 'none';

      // Clear topics container
      topicsContainer.innerHTML = '';
      if(!topicsData[category]) {
        topicsContainer.innerHTML = '<p>No topics found.</p>';
        return;
      }
      topicsData[category].forEach(topic => {
        const btn = document.createElement('button');
        btn.textContent = topic;
        btn.className = 'topic-btn';
        btn.onclick = () => showBooksList(topic);
        topicsContainer.appendChild(btn);
      });
    }

    function showBooksList(topic) {
      currentTopic = topic;
      document.getElementById('home-screen').style.display = 'none';
      document.getElementById('book-screen').style.display = 'none';
      document.getElementById('topics-screen').style.display = 'none';
      booksListScreen.style.display = 'block';
      bookDetailScreen.style.display = 'none';

      listHeading.textContent = `${topic} Books`;
      renderBooksList(topic);
    }

    /* ---------- RENDER BOOKS ---------- */
    function renderBooksList(topic) {
      booksListEl.innerHTML = '';

      let booksArray = [];

      // For demo, only kids > "Hindu Mythology & Epics" has data
      if(topic === "Hindu Mythology & Epics"){
        booksArray = mythBooks;
      }

      if(booksArray.length === 0){
        booksListEl.innerHTML = '<p>No books available in this topic yet.</p>';
        return;
      }

      booksArray.forEach(book => {
        const card = document.createElement('div');
        card.className = 'book-card';
        card.innerHTML = `
          <img src="${book.image}" alt="${book.title}" />
          <div class="book-info">
            <h4>${book.title}</h4>
            ${book.price ? `<div class="small-price">₹${book.price}</div>` : ''}
          </div>
        `;
        card.onclick = () => showBookDetail(book);
        booksListEl.appendChild(card);
      });
    }

    function showBookDetail(book) {
      booksListScreen.style.display = 'none';
      bookDetailScreen.style.display = 'block';

      bookDetailEl.innerHTML = `
        <div class="book-detail-wrapper">
          <img src="${book.image}" alt="${book.title}" />
          <div class="book-detail-info">
            <h3>${book.title}</h3>
            ${book.price ? `<p class="price-tag">₹${book.price}</p>` : ''}
            <p>${book.desc || "No description available."}</p>
            <button class="action-btn">Subscribe Now</button>
          </div>
        </div>
      `;
    }

    function backToList() {
      bookDetailScreen.style.display = 'none';
      booksListScreen.style.display = 'block';
    }

    /* ---------- SEARCH FUNCTION ---------- */
    function handleSearch(event) {
      const query = event.target.value.toLowerCase();
      if(!query){
        booksListScreen.style.display = 'none';
        showHome();
        return;
      }

      // For demo, search only Hindu Mythology books
      const results = mythBooks.filter(book => book.title.toLowerCase().includes(query));
      if(results.length === 0){
        booksListEl.innerHTML = `<p>No results found for "${query}"</p>`;
      } else {
        booksListEl.innerHTML = '';
        results.forEach(book => {
          const card = document.createElement('div');
          card.className = 'book-card';
          card.innerHTML = `
            <img src="${book.image}" alt="${book.title}" />
            <div class="book-info">
              <h4>${book.title}</h4>
              ${book.price ? `<div class="small-price">₹${book.price}</div>` : ''}
            </div>
          `;
          card.onclick = () => showBookDetail(book);
          booksListEl.appendChild(card);
        });
      }

      document.getElementById('home-screen').style.display = 'none';
      document.getElementById('book-screen').style.display = 'none';
      document.getElementById('topics-screen').style.display = 'none';
      booksListScreen.style.display = 'block';
      bookDetailScreen.style.display = 'none';
    }

    /* ---------- CONTACT FORM ---------- */
    function handleContactForm(event) {
      event.preventDefault();
      alert('Thank you for contacting StoryGems!');
      event.target.reset();
    }

    /* ---------- LOGIN FUNCTIONS ---------- */
    function handleLogin() {
      const username = document.getElementById('username').value.trim();
      const password = document.getElementById('password').value.trim();
      if(!username || !password) {
        alert('Please enter both username and password');
        return;
      }
      // You can add real auth here later
      document.body.classList.remove('logged-out');
      loginScreen.style.display = 'none';
      alert(`Welcome, ${username}!`);
    }

    function continueAsGuest() {
      document.body.classList.remove('logged-out');
      loginScreen.style.display = 'none';
      alert('Continuing as guest');
    }

    // On page load, show home by default if main content is visible
    if(!document.body.classList.contains('logged-out')){
      showHome();
    }
  </script>
</body>
</html>
