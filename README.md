<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: system-ui, -apple-system, sans-serif;
      margin: 0;
      padding: 16px;
      background: #f5f5f5;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      background: white;
      padding: 24px;
      border-radius: 12px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }
    .search-bar {
      position: relative;
      margin-bottom: 16px;
    }
    input {
      width: 100%;
      padding: 12px 12px 12px 40px;
      border: 1px solid #ddd;
      border-radius: 8px;
      font-size: 16px;
      box-sizing: border-box;
    }
    .search-icon {
      position: absolute;
      left: 12px;
      top: 50%;
      transform: translateY(-50%);
      color: #666;
    }
    .filter-buttons {
      display: flex;
      gap: 8px;
      margin-bottom: 16px;
    }
    .btn {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 8px 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
      background: #f3f4f6;
      color: #374151;
      transition: all 0.3s ease;
    }
    .btn.active {
      background: #0d9488;
      color: white;
    }
    .btn.active svg {
      color: white;
    }
    .region-dropdown {
      width: 100%;
      padding: 12px;
      border: 1px solid #ddd;
      border-radius: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: #f9fafb;
      margin-bottom: 16px;
      cursor: pointer;
    }
    .title {
      font-size: 24px;
      font-weight: 600;
      margin-bottom: 8px;
    }
    .subtitle {
      color: #666;
      margin-bottom: 24px;
    }
    svg {
      width: 20px;
      height: 20px;
      color: #666;
      transition: color 0.3s ease;
    }
    .regions-grid {
      display: none;
      margin-top: 8px;
      padding: 16px;
      border: 1px solid #ddd;
      border-radius: 8px;
      background: white;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    .regions-grid.show {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 8px;
    }
    .region-btn {
      padding: 8px;
      border: none;
      border-radius: 6px;
      background: #f3f4f6;
      color: #374151;
      cursor: pointer;
      text-align: left;
      display: flex;
      align-items: center;
    }
    .region-btn:hover {
      background: #e5e7eb;
    }
    .region-btn.selected {
      background: #0d9488;
      color: white;
    }
    .chevron {
      transition: transform 0.3s ease;
    }
    .chevron.rotate {
      transform: rotate(180deg);
    }
    .zone-id {
      font-weight: bold;
      margin-right: 8px;
      min-width: 45px;
    }
    .bottom-search-button {
      width: 100%;
      padding: 16px;
      background: #0d9488;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      margin-top: 16px;
    }
    .bottom-search-button svg {
      color: white;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="title">Master Tung's Points</div>
    <div class="subtitle">Search by point name, indications, or reaction area</div>
    
    <div class="search-bar">
      <svg xmlns="http://www.w3.org/2000/svg" class="search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <circle cx="11" cy="11" r="8"></circle>
        <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
      </svg>
      <input type="text" placeholder="Search points, indications, or areas...">
    </div>
    
    <div class="filter-buttons">
      <button class="btn" onclick="setActiveButton(this, 'all')">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="4" y1="21" x2="4" y2="14"></line>
          <line x1="4" y1="10" x2="4" y2="3"></line>
          <line x1="12" y1="21" x2="12" y2="12"></line>
          <line x1="12" y1="8" x2="12" y2="3"></line>
          <line x1="20" y1="21" x2="20" y2="16"></line>
          <line x1="20" y1="12" x2="20" y2="3"></line>
          <line x1="1" y1="14" x2="7" y2="14"></line>
          <line x1="9" y1="8" x2="15" y2="8"></line>
          <line x1="17" y1="16" x2="23" y2="16"></line>
        </svg>
        All
      </button>
      <button class="btn" onclick="setActiveButton(this, 'indications')">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="22 12 18 12 15 21 9 3 6 12 2 12"></polyline>
        </svg>
        Indications
      </button>
      <button class="btn" onclick="setActiveButton(this, 'area')">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="12" cy="12" r="10"></circle>
          <circle cx="12" cy="12" r="6"></circle>
          <circle cx="12" cy="12" r="2"></circle>
        </svg>
        Reaction Area
      </button>
    </div>
    
    <button id="regionDropdown" class="region-dropdown">
      <span style="display: flex; align-items: center; gap: 8px;">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
          <circle cx="12" cy="10" r="3"></circle>
        </svg>
        Zone
      </span>
      <svg class="chevron" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <polyline points="6 9 12 15 18 9"></polyline>
      </svg>
    </button>

    <div id="regionsGrid" class="regions-grid">
      <button class="region-btn"><span class="zone-id">11</span><span>Fingers</span></button>
      <button class="region-btn"><span class="zone-id">22</span><span>Hand</span></button>
      <button class="region-btn"><span class="zone-id">33</span><span>Forearm</span></button>
      <button class="region-btn"><span class="zone-id">44</span><span>Arm</span></button>
      <button class="region-btn"><span class="zone-id">55</span><span>Sole</span></button>
      <button class="region-btn"><span class="zone-id">66</span><span>Feet</span></button>
      <button class="region-btn"><span class="zone-id">77</span><span>Calve</span></button>
      <button class="region-btn"><span class="zone-id">88</span><span>Thigh</span></button>
      <button class="region-btn"><span class="zone-id">99</span><span>Ear</span></button>
      <button class="region-btn"><span class="zone-id">1010</span><span>Face</span></button>
      <button class="region-btn"><span class="zone-id">VT</span><span>Chest and abdomen</span></button>
      <button class="region-btn"><span class="zone-id">DT</span><span>Back and neck</span></button>
    </div>

    <!-- Search Button -->
    <button class="bottom-search-button">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <circle cx="11" cy="11" r="8"></circle>
        <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
      </svg>
      Search
    </button>
  </div>

  <script>
    const dropdown = document.getElementById('regionDropdown');
    const regionsGrid = document.getElementById('regionsGrid');
    const chevron = document.querySelector('.chevron');
    const regionBtns = document.querySelectorAll('.region-btn');

    dropdown.addEventListener('click', () => {
      regionsGrid.classList.toggle('show');
      chevron.classList.toggle('rotate');
    });

    regionBtns.forEach(btn => {
      btn.addEventListener('click', (e) => {
        e.stopPropagation();
        btn.classList.toggle('selected');
      });
    });

    function setActiveButton(clickedBtn, type) {
      document.querySelectorAll('.filter-buttons .btn').forEach(btn => {
        btn.classList.remove('active');
      });
      
      clickedBtn.classList.add('active');

      const searchInput = document.querySelector('input');
      if (type === 'all') {
        searchInput.placeholder = "Search points, indications, or areas...";
      } else if (type === 'indications') {
        searchInput.placeholder = "Search by indications...";
      } else if (type === 'area') {
        searchInput.placeholder = "Search by reaction area...";
      }
    }

    document.querySelector('.filter-buttons .btn').classList.add('active');
  </script>
</body>
</html>
