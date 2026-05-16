# beast-pro
media searcher
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Beast PRO // Universal Downloader & Streamer</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700;900&family=Space+Grotesk:wght@700&display=swap" rel="stylesheet">
  <style>
    :root {
      --vidmate-red: #ff2a44;
      /* Iconic VidMate Cherry Red */
      --vidmate-orange: #ff6a00;
      --bg-base: #f7f8fa;
      /* Soft light grey mobile app background */
      --bg-surface: #ffffff;
      --text-main: #1a1a1a;
      --text-muted: #8c8c8c;
      --border-color: #e8eaf0;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Roboto', sans-serif;
      background-color: var(--bg-base);
      color: var(--text-main);
      overflow-x: hidden;
    }

    /* --- CINEMATIC APP SPLASH SCREEN LAYER --- */
    #appSplashScreen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-color: #ffffff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 9999;
      transition: opacity 0.8s cubic-bezier(0.25, 1, 0.5, 1), visibility 0.8s;
    }

    .splash-container {
      text-align: center;
      max-width: 280px;
      width: 100%;
    }

    .splash-logo {
      width: 200px;
      height: 200px;
      object-fit: contain;
      margin-bottom: 15px;
    }

    .splash-title {
      font-family: 'Space Grotesk', sans-serif;
      color: #1a1a1a;
      font-size: 26px;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-bottom: 8px;
    }

    .splash-title span {
      color: var(--vidmate-red);
    }

    .splash-subtitle {
      color: #a1a1aa;
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: 2px;
      margin-bottom: 35px;
    }

    .loading-bar-track {
      width: 100%;
      height: 4px;
      background: rgba(0, 0, 0, 0.08);
      border-radius: 2px;
      overflow: hidden;
      position: relative;
    }

    .loading-bar-progress {
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, var(--vidmate-red), var(--vidmate-orange));
      border-radius: 2px;
      animation: appBootSequence 10s linear forwards;
    }

    @keyframes appBootSequence {
      0% {
        width: 0%;
      }

      15% {
        width: 20%;
      }

      50% {
        width: 55%;
      }

      75% {
        width: 85%;
      }

      100% {
        width: 100%;
      }
    }

    /* --- DYNAMIC CONTEXTUAL SCREENSAVER LAYER --- */
    #appScreensaver {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-color: rgba(5, 5, 6, 0.96);
      /* Immersive dark cinematic backplane */
      z-index: 5000;
      align-items: center;
      justify-content: center;
      opacity: 0;
      transition: opacity 0.6s ease;
      cursor: pointer;
      user-select: none;
    }

    #appScreensaver.active {
      display: flex;
      opacity: 1;
    }

    .screensaver-content {
      text-align: center;
      color: #ffffff;
      max-width: 80%;
      animation: screensaverFloat 8s ease-in-out infinite alternate;
    }

    .screensaver-media-frame {
      width: 260px;
      height: 260px;
      margin: 0 auto 20px auto;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8), 0 0 40px rgba(255, 42, 68, 0.15);
      background: #000;
    }

    .screensaver-media-frame img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .screensaver-title {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 22px;
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-bottom: 8px;
      color: #ffffff;
    }

    .screensaver-subtext {
      font-size: 13px;
      color: var(--vidmate-red);
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 2px;
    }

    .screensaver-hint {
      position: absolute;
      bottom: 30px;
      font-size: 11px;
      color: #555;
      text-transform: uppercase;
      letter-spacing: 1px;
      width: 100%;
      text-align: center;
    }

    @keyframes screensaverFloat {
      0% {
        transform: translateY(0px) scale(0.98);
      }

      100% {
        transform: translateY(-15px) scale(1.02);
      }
    }

    /* --- VIDMATE MOBILE APP TOP BANNER --- */
    header {
      background: linear-gradient(135deg, var(--vidmate-red) 0%, var(--vidmate-orange) 100%);
      padding: 14px 16px;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 3px 10px rgba(255, 42, 68, 0.2);
    }

    .header-container {
      max-width: 600px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .brand-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .brand-row h1 {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 24px;
      font-weight: 700;
      color: #ffffff;
      text-transform: uppercase;
      letter-spacing: -0.5px;
    }

    .brand-row h1 span {
      font-family: 'Roboto', sans-serif;
      font-weight: 700;
      font-size: 12px;
      background: #ffffff;
      color: var(--vidmate-red);
      padding: 2px 6px;
      border-radius: 4px;
      margin-left: 6px;
      vertical-align: middle;
    }

    /* --- SEARCH PIPELINE BAR --- */
    .search-bar-wrapper {
      position: relative;
      display: flex;
      align-items: center;
    }

    .search-input {
      width: 100%;
      background: #ffffff;
      border: none;
      padding: 12px 16px;
      padding-right: 50px;
      border-radius: 24px;
      color: #333;
      font-size: 14px;
      font-weight: 500;
      outline: none;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
    }

    .search-submit-btn {
      position: absolute;
      right: 6px;
      background: var(--vidmate-red);
      color: #fff;
      border: none;
      width: 34px;
      height: 34px;
      border-radius: 50%;
      font-weight: bold;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    /* --- HORIZONTAL SCROLLING CATEGORY CHIPS --- */
    .category-scroll-deck {
      background: var(--bg-surface);
      border-bottom: 1px solid var(--border-color);
      padding: 0 8px;
      display: flex;
      overflow-x: auto;
      white-space: nowrap;
      scrollbar-width: none;
    }

    .category-scroll-deck::-webkit-scrollbar {
      display: none;
    }

    .scroll-item-btn {
      background: transparent;
      border: none;
      color: #555;
      padding: 14px 16px;
      font-size: 15px;
      font-weight: 700;
      cursor: pointer;
      position: relative;
      display: inline-block;
    }

    .scroll-item-btn.active {
      color: var(--vidmate-red);
    }

    .scroll-item-btn.active::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 25%;
      width: 50%;
      height: 3px;
      background: var(--vidmate-red);
      border-radius: 2px 2px 0 0;
    }

    /* --- MAIN HIGH DENSITY MEDIA GRID --- */
    .main-wrapper {
      max-width: 600px;
      margin: 0 auto;
      padding: 12px;
    }

    .grid-matrix {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 10px;
    }

    /* --- VIDMATE CARD ARCHITECTURE --- */
    .media-card {
      background: var(--bg-surface);
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 1px 4px rgba(0, 0, 0, 0.04);
      display: flex;
      flex-direction: column;
      cursor: pointer;
    }

    .poster-frame {
      width: 100%;
      padding-top: 56.25%;
      position: relative;
      background: #e1e1e1;
    }

    .poster-frame img {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .stream-hd-tag {
      position: absolute;
      bottom: 6px;
      right: 6px;
      background: rgba(0, 0, 0, 0.75);
      color: #fff;
      font-size: 11px;
      padding: 2px 4px;
      border-radius: 2px;
      font-weight: bold;
    }

    .stream-type-tag {
      position: absolute;
      top: 6px;
      left: 6px;
      background: var(--vidmate-red);
      color: #fff;
      font-size: 10px;
      padding: 1px 5px;
      border-radius: 2px;
      font-weight: 700;
      text-transform: uppercase;
    }

    .card-details {
      padding: 8px 10px 12px 10px;
    }

    .card-title {
      font-size: 13px;
      font-weight: 500;
      color: var(--text-main);
      line-height: 1.4;
      height: 36px;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      overflow: hidden;
      margin-bottom: 6px;
    }

    .card-subtext {
      font-size: 11px;
      color: var(--text-muted);
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    /* --- LIGHTBOX MODAL --- */
    .lightbox-modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.9);
      z-index: 1000;
      align-items: center;
      justify-content: center;
      padding: 12px;
    }

    .lightbox-modal.active {
      display: flex;
    }

    .modal-wrapper-box {
      width: 100%;
      max-width: 550px;
      background: var(--bg-surface);
      border-radius: 12px;
      overflow: hidden;
      position: relative;
    }

    .close-modal-btn {
      position: absolute;
      top: 10px;
      right: 10px;
      background: rgba(0, 0, 0, 0.6);
      border: none;
      color: #fff;
      width: 32px;
      height: 32px;
      border-radius: 50%;
      cursor: pointer;
      z-index: 110;
      font-weight: bold;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .player-container {
      width: 100%;
      padding-top: 56.25%;
      background: #000;
      position: relative;
    }

    .player-container iframe,
    .player-container img {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }

    .cancel-stream-btn {
      position: absolute;
      bottom: 12px;
      right: 12px;
      background: var(--vidmate-red);
      color: #ffffff;
      border: none;
      padding: 8px 14px;
      border-radius: 20px;
      font-size: 11px;
      font-weight: 700;
      text-transform: uppercase;
      cursor: pointer;
      z-index: 120;
      box-shadow: 0 3px 8px rgba(255, 42, 68, 0.4);
    }

    .modal-info-panel {
      padding: 16px;
    }

    .modal-meta {
      margin-top: 6px;
      font-size: 12px;
      color: var(--vidmate-red);
      font-weight: bold;
    }
  </style>
</head>

<body>

  <div id="appSplashScreen">
    <div class="splash-container">
      <img class="splash-logo" src="download (3).jpg" alt="Beast PRO Engine">
      <div class="splash-title">Beast <span>PRO</span></div>
      <div class="splash-subtitle">Media Deck Architecture</div>
      <div class="loading-bar-track">
        <div class="loading-bar-progress"></div>
      </div>
    </div>
  </div>

  <div id="appScreensaver" onclick="wakeDeviceUp()">
    <div class="screensaver-content">
      <div class="screensaver-media-frame" id="screensaverVisualCore">
      </div>
      <div class="screensaver-title" id="screensaverTitleCore">FEED THE BEAST</div>
      <div class="screensaver-subtext" id="screensaverMetaCore">AMBIENT STANDBY ACTIVE</div>
    </div>
    <div class="screensaver-hint">Press or Tap anywhere to resume stream deck</div>
  </div>

  <header>
    <div class="header-container">
      <div class="brand-row">
        <h1>Beast <span>PRO</span></h1>
      </div>
      <div class="search-bar-wrapper">
        <input type="text" id="mainSearchInput" class="search-input" placeholder="Search or enter URL to download..." onkeypress="if(event.key==='Enter') executePipelineSearch()">
        <button class="search-submit-btn" id="pipelineSearchBtn" onclick="executePipelineSearch()">🔍</button>
      </div>
    </div>
  </header>

  <div class="category-scroll-deck">
    <button class="scroll-item-btn active" data-type="movies" onclick="setMediaType('movies')">Featured Movies</button>
    <button class="scroll-item-btn" data-type="videos" onclick="setMediaType('videos')">YouTube Videos</button>
    <button class="scroll-item-btn" data-type="images" onclick="setMediaType('images')">Wallpapers & Pics</button>
  </div>

  <main class="main-wrapper">
    <div class="grid-matrix" id="catalogResultsMatrix"></div>
  </main>

  <div class="lightbox-modal" id="mediaLightbox">
    <div class="modal-wrapper-box">
      <button class="close-modal-btn" onclick="closeMediaLightbox()">✕</button>
      <div class="player-container" id="lightboxPlayerView">
      </div>
      <div class="modal-info-panel">
        <h3 id="modalMediaTitle">Loading Feed...</h3>
        <div class="modal-meta" id="modalMediaMeta">Beast PRO Media Pipeline Loaded</div>
      </div>
    </div>
  </div>

  <script>
    const OMDB_API_KEY = "74cba55c";
    const PEXELS_API_KEY = "H6MkkgrYvaiKEt4gFPmYg5LvaPkOCizh9ar6wGKAdiqZdCx4Nokp1v5O";
    const YOUTUBE_API_KEY = "AIzaSyC-fUWy_25ZiaeOYGm6tlAIX8yHlecCcf4";
    let currentPipelineMode = "movies";
    let splashActive = true;
    // Smart history state collection arrays
    let userViewHistory = {
      title: "FEED THE BEAST",
      meta: "SYSTEM IDLE // DATA ENGINE STANDBY",
      imageUrl: "download (3).jpg"
    };
    // Standby Idle Timer Monitor Metrics
    let idleTimerToken;
    const STANDBY_TIMEOUT_THRESHOLD = 10000; // Locked to exactly 10 Seconds of zero interactions
    window.onload = () => {
      setTimeout(() => {
        const splashScreen = document.getElementById("appSplashScreen");
        splashScreen.style.opacity = "0";
        setTimeout(() => {
          splashScreen.style.visibility = "hidden";
          splashActive = false;
          resetIdleSystemTimer(); // Start tracking idle states after splash screen ends
        }, 800);
      }, 10000);
      executePipelineSearch();
      setupInteractionListeners();
    };
    /* --- SCREENSAVER LOGIC CENTER --- */
    function setupInteractionListeners() {
      // Listen to all forms of screen interaction to block/reset screen saver execution
      const activityEvents = ['mousedown', 'mousemove', 'keypress', 'scroll', 'touchstart'];
      activityEvents.forEach(eventName => {
        document.addEventListener(eventName, resetIdleSystemTimer, true);
      });
    }

    function resetIdleSystemTimer() {
      if (splashActive) return; // Prevent early startup triggers while loading screen is up
      clearTimeout(idleTimerToken);
      // Check if the user is currently in standby mode before calculating new clock tracks
      const saverLayer = document.getElementById("appScreensaver");
      if (saverLayer.classList.contains("active")) {
        wakeDeviceUp();
      }
      idleTimerToken = setTimeout(engageScreensaverStandby, STANDBY_TIMEOUT_THRESHOLD);
    }

    function engageScreensaverStandby() {
      // Map current dynamic history tracking into screensaver framework arrays
      document.getElementById("screensaverVisualCore").innerHTML = `<img src="${userViewHistory.imageUrl}">`;
      document.getElementById("screensaverTitleCore").innerText = userViewHistory.title;
      document.getElementById("screensaverMetaCore").innerText = userViewHistory.meta;
      const saverLayer = document.getElementById("appScreensaver");
      saverLayer.style.display = "flex";
      setTimeout(() => {
        saverLayer.classList.add("active");
      }, 20);
    }

    function wakeDeviceUp() {
      const saverLayer = document.getElementById("appScreensaver");
      saverLayer.classList.remove("active");
      setTimeout(() => {
        saverLayer.style.display = "none";
      }, 600);
      // Restart search deck clock loop tracker
      clearTimeout(idleTimerToken);
      idleTimerToken = setTimeout(engageScreensaverStandby, STANDBY_TIMEOUT_THRESHOLD);
    }
    /* --- API DATA PIPELINES & PARSERS --- */
    function setMediaType(type) {
      currentPipelineMode = type;
      document.querySelectorAll('.scroll-item-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelector(`.scroll-item-btn[data-type="${type}"]`).classList.add('active');
      const placeholderField = document.getElementById("mainSearchInput");
      if (type === "movies") {
        placeholderField.placeholder = "Search trending OMDb film files...";
      } else if (type === "images") {
        placeholderField.placeholder = "Search wallpapers, images, graphics...";
      } else {
        placeholderField.placeholder = "Search or paste streaming YouTube URL...";
      }
      executePipelineSearch();
    }
    async function executePipelineSearch() {
      const searchString = document.getElementById("mainSearchInput").value.trim();
      const targetOutputContainer = document.getElementById("catalogResultsMatrix");
      targetOutputContainer.innerHTML = `<div style="grid-column: span 2; text-align:center; padding:30px; color:var(--text-muted); font-size:14px;">Fetching trending feeds...</div>`;
      if (currentPipelineMode === "movies") {
        const queryTerm = searchString || "Marvel";
        const endpoint = `https://www.omdbapi.com/?s=${encodeURIComponent(queryTerm)}&apikey=${OMDB_API_KEY}`;
        try {
          const response = await fetch(endpoint);
          const data = await response.json();
          targetOutputContainer.innerHTML = "";
          if (data.Response === "False" || !data.Search) {
            targetOutputContainer.innerHTML = `<div style="grid-column: span 2; text-align:center; color:var(--text-muted)">No media found matching keywords.</div>`;
            return;
          }
          // Log first match into history fallback matrix instantly
          if (data.Search[0]) {
            userViewHistory = {
              title: data.Search[0].Title,
              meta: `Trending History Core // Year: ${data.Search[0].Year}`,
              imageUrl: data.Search[0].Poster
            };
          }
          data.Search.forEach((movie) => {
            if (movie.Poster === "N/A") return;
            const cardItem = document.createElement("div");
            cardItem.className = "media-card";
            cardItem.onclick = () => {
              // Update user runtime history stack on card interaction
              userViewHistory = {
                title: movie.Title,
                meta: `LAST VIEWED MOVIE NODE // ${movie.Year}`,
                imageUrl: movie.Poster
              };
              launchLiveMovieDetail(movie.imdbID);
            };
            cardItem.innerHTML = `
                    <div class="poster-frame">
                        <img src="${movie.Poster}" alt="media preview">
                        <span class="stream-type-tag">Movie</span>
                        <span class="stream-hd-tag">HD 1080P</span>
                    </div>
                    <div class="card-details">
                        <div class="card-title">${movie.Title}</div>
                        <div class="card-subtext">${movie.Year} // ${movie.Type}</div>
                    </div>`;
            targetOutputContainer.appendChild(cardItem);
          });
        } catch (e) {
          targetOutputContainer.innerHTML = `<div style="grid-column: span 2; text-align:center; color:red">Failed to reach film source gateway.</div>`;
        }
      } else if (currentPipelineMode === "images") {
        const imageQuery = searchString || "Nature Wallpaper";
        const endpoint = `https://api.pexels.com/v1/search?query=${encodeURIComponent(imageQuery)}&per_page=16`;
        try {
          const response = await fetch(endpoint, {
            headers: {
              Authorization: PEXELS_API_KEY
            }
          });
          const data = await response.json();
          targetOutputContainer.innerHTML = "";
          if (!data.photos || data.photos.length === 0) {
            targetOutputContainer.innerHTML = `<div style="grid-column: span 2; text-align:center; color:var(--text-muted)">No image nodes located.</div>`;
            return;
          }
          if (data.photos[0]) {
            userViewHistory = {
              title: `Wallpaper by ${data.photos[0].photographer}`,
              meta: "Active Background Vector Target",
              imageUrl: data.photos[0].src.large
            };
          }
          data.photos.forEach((photo) => {
            const cardItem = document.createElement("div");
            cardItem.className = "media-card";
            cardItem.onclick = () => {
              userViewHistory = {
                title: `Captured by ${photo.photographer}`,
                meta: `HD STANDBY BACKDROP // ${photo.width}x${photo.height}`,
                imageUrl: photo.src.large
              };
              launchLiveImageDetail(photo.src.large2x, photo.photographer);
            };
            cardItem.innerHTML = `
                    <div class="poster-frame">
                        <img src="${photo.src.medium}" alt="pexels target">
                        <span class="stream-type-tag" style="background:#00bcd4">IMG</span>
                        <span class="stream-hd-tag">4K ULTRA</span>
                    </div>
                    <div class="card-details">
                        <div class="card-title">By ${photo.photographer}</div>
                        <div class="card-subtext">Res: ${photo.width}x${photo.height}</div>
                    </div>`;
            targetOutputContainer.appendChild(cardItem);
          });
        } catch (e) {
          targetOutputContainer.innerHTML = `<div style="grid-column: span 2; text-align:center; color:red">Failed to process wallpaper assets.</div>`;
        }
      } else {
        const videoQuery = searchString || "New Movie Trailers 2026";
        const endpoint = `https://www.googleapis.com/youtube/v3/search?part=snippet&q=${encodeURIComponent(videoQuery)}&type=video&maxResults=16&key=${YOUTUBE_API_KEY}`;
        try {
          const response = await fetch(endpoint);
          const data = await response.json();
          targetOutputContainer.innerHTML = "";
          if (data.error || !data.items || data.items.length === 0) {
            targetOutputContainer.innerHTML = `<div style="grid-column: span 2; text-align:center; color:var(--text-muted)">No video streams running. Check API connectivity status.</div>`;
            return;
          }
          if (data.items[0]) {
            userViewHistory = {
              title: data.items[0].snippet.title,
              meta: `Youtube Core Stream // ${data.items[0].snippet.channelTitle}`,
              imageUrl: data.items[0].snippet.thumbnails.high.url
            };
          }
          data.items.forEach((item) => {
            const cardItem = document.createElement("div");
            cardItem.className = "media-card";
            cardItem.onclick = () => {
              userViewHistory = {
                title: item.snippet.title,
                meta: `STREAM FEED STANDBY // ${item.snippet.channelTitle}`,
                imageUrl: item.snippet.thumbnails.high.url
              };
              launchLiveVideoPlayer(item.id.videoId, item.snippet.title, item.snippet.channelTitle);
            };
            cardItem.innerHTML = `
                    <div class="poster-frame">
                        <img src="${item.snippet.thumbnails.high.url}" alt="thumbnail">
                        <span class="stream-type-tag" style="background:#4caf50">MP4</span>
                        <span class="stream-hd-tag">720P HD</span>
                    </div>
                    <div class="card-details">
                        <div class="card-title">${item.snippet.title}</div>
                        <div class="card-subtext">${item.snippet.channelTitle}</div>
                    </div>`;
            targetOutputContainer.appendChild(cardItem);
          });
        } catch (e) {
          targetOutputContainer.innerHTML = `<div style="grid-column: span 2; text-align:center; color:red">YouTube API gateway disconnected.</div>`;
        }
      }
    }
    async function launchLiveMovieDetail(imdbID) {
      const playerView = document.getElementById("lightboxPlayerView");
      playerView.innerHTML = `<div style="position:absolute; width:100%; text-align:center; color:#fff; top:45%;">Opening media thread...</div>`;
      document.getElementById("mediaLightbox").classList.add("active");
      try {
        const res = await fetch(`https://www.omdbapi.com/?i=${imdbID}&apikey=${OMDB_API_KEY}`);
        const filmData = await res.json();
        document.getElementById("modalMediaTitle").innerText = filmData.Title;
        document.getElementById("modalMediaMeta").innerText = `Year: ${filmData.Year} // Genre: ${filmData.Genre}`;
        playerView.innerHTML = `
            <img src="${filmData.Poster}" style="width:100%; height:100%; object-fit:contain;">
            <button class="cancel-stream-btn" onclick="closeMediaLightbox()">🛑 Stop Play</button>
        `;
      } catch (e) {
        playerView.innerHTML = `<div style="color:red; text-align:center; padding:20px;">Stream Initialization Failure.</div>`;
      }
    }

    function launchLiveImageDetail(highResUrl, photographer) {
      document.getElementById("modalMediaTitle").innerText = `Wallpaper by ${photographer}`;
      document.getElementById("modalMediaMeta").innerText = `Source: Pexels Core Library`;
      const playerView = document.getElementById("lightboxPlayerView");
      playerView.innerHTML = `
        <img src="${highResUrl}" style="width:100%; height:100%; object-fit:contain;">
        <button class="cancel-stream-btn" onclick="closeMediaLightbox()">✕ Close</button>
    `;
      document.getElementById("mediaLightbox").classList.add("active");
    }

    function launchLiveVideoPlayer(youtubeId, title, channelTitle) {
      document.getElementById("modalMediaTitle").innerText = title;
      document.getElementById("modalMediaMeta").innerText = `Publisher: ${channelTitle}`;
      const playerView = document.getElementById("lightboxPlayerView");
      playerView.innerHTML = `
        <iframe 
            src="https://www.youtube.com/embed/${youtubeId}?autoplay=1" 
            allow="autoplay; encrypted-media; picture-in-picture" 
            sandbox="allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-same-origin allow-scripts"
            allowfullscreen>
        </iframe>
        <button class="cancel-stream-btn" onclick="closeMediaLightbox()">🛑 Cancel Stream</button>
    `;
      document.getElementById("mediaLightbox").classList.add("active");
    }

    function closeMediaLightbox() {
      document.getElementById("mediaLightbox").classList.remove("active");
      document.getElementById("lightboxPlayerView").innerHTML = "";
    }
  </script>
</body>

</html>[index.html.txt](https://github.com/user-attachments/files/27853663/index.html.txt)
