# redesigned-meme
<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>LINERAW 街舞活動資訊</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC&display=swap');
  /* Reset and base */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    font-family: 'Noto Sans TC', sans-serif;
    background: linear-gradient(135deg, #3a9bdc, #1f5377);
    color: #e0f0ff;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  header {
    background: #0f3550;
    padding: 1.5rem 1rem;
    text-align: center;
    box-shadow: 0 2px 10px rgba(0,0,0,0.4);
  }
  header h1 {
    margin: 0;
    font-size: 2.6rem;
    letter-spacing: 0.15em;
    text-shadow: 0 2px 6px rgba(0,0,0,0.8);
  }
  header p.slogan {
    margin: 0.3rem 0 0 0;
    font-size: 1.2rem;
    font-style: italic;
    color: #a3d1ff;
    text-shadow: 0 1px 3px rgba(0,0,0,0.6);
  }
  main {
    flex-grow: 1;
    display: flex;
    flex-wrap: wrap;
    padding: 1rem;
    max-width: 1200px;
    margin: 1rem auto 2rem auto;
    background: rgba(255, 255, 255, 0.05);
    border-radius: 10px;
    box-shadow: 0 0 20px #1460a0aa;
  }
  section.form-section, section.events-section {
    background: rgba(10,30,60,0.5);
    border-radius: 10px;
    padding: 1rem 1.5rem;
    box-shadow: inset 0 0 10px #0c2a54;
  }
  section.form-section {
    flex: 1 1 350px;
    max-width: 400px;
    margin-right: 1.5rem;
  }
  section.form-section h2 {
    margin-top: 0;
    font-size: 1.6rem;
    border-bottom: 2px solid #48a9e6;
    padding-bottom: 0.3rem;
    color: #87cefa;
  }
  label {
    display: block;
    margin-top: 0.8rem;
    font-weight: 600;
    font-size: 0.95rem;
    color: #bcd8f7;
  }
  input[type="text"],
  input[type="datetime-local"],
  select,
  textarea {
    width: 100%;
    margin-top: 0.25rem;
    padding: 8px 10px;
    border-radius: 6px;
    border: none;
    font-size: 1rem;
    font-family: 'Noto Sans TC', sans-serif;
  }
  textarea {
    resize: vertical;
  }
  button {
    margin-top: 1.2rem;
    background: #2ca4f0;
    color: white;
    border: none;
    padding: 12px 20px;
    font-size: 1.1rem;
    border-radius: 10px;
    cursor: pointer;
    box-shadow: 0 3px 8px #0b5295;
    transition: background-color 0.25s ease;
  }
  button:hover {
    background: #3cb0ff;
  }
  section.events-section {
    flex: 2 1 600px;
    min-width: 300px;
    display: flex;
    flex-direction: column;
  }
  .controls {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    align-items: center;
    margin-bottom: 1rem;
  }
  .controls > * {
    flex-grow: 1;
    min-width: 130px;
  }
  .events-list {
    overflow-y: auto;
    max-height: 520px;
    background: rgba(15,60,100,0.35);
    border-radius: 10px;
    padding: 0.8rem;
    color: #cce6ff;
    box-shadow: inset 0 0 12px #154a78;
  }
  .event-item {
    background: rgba(26, 70, 120, 0.7);
    padding: 0.9rem 1.2rem;
    margin-bottom: 10px;
    border-radius: 8px;
    box-shadow: 0 2px 6px #1b4a89cc;
    transition: background-color 0.3s ease;
  }
  .event-item:hover {
    background-color: rgba(40, 110, 180, 0.8);
  }
  .event-name {
    font-size: 1.3rem;
    font-weight: 700;
    color: #d1eaff;
  }
  .event-time {
    font-size: 0.9rem;
    font-style: italic;
    margin: 0.15rem 0;
    color: #a0c8ff;
  }
  .event-location {
    font-size: 1rem;
    font-weight: 600;
    color: #b2d1ff;
  }
  .event-intro {
    margin-top: 0.4rem;
    font-size: 0.95rem;
    color: #d4eafd;
  }
  .event-link {
    margin-top: 0.5rem;
    display: inline-block;
    color: #61a5ff;
    text-decoration: underline;
  }
  .filter-region {
    text-align: center;
  }
  .filter-region button {
    flex-grow: 0;
    margin: 0 6px 6px 0;
    background: #0b4f85;
  }
  .filter-region button.active {
    background: #49a7f7;
    box-shadow: 0 0 10px #7ad1ff;
  }
  /* Calendar styles */
  .calendar-view {
    overflow-y: auto;
    max-height: 520px;
    background: rgba(15,60,100,0.35);
    border-radius: 10px;
    padding: 0.8rem;
    color: #cce6ff;
    box-shadow: inset 0 0 12px #154a78;
    user-select: none;
  }
  .calendar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }
  .calendar-header h3 {
    margin: 0;
    font-weight: 700;
    font-size: 1.4rem;
    color: #ace1ff;
  }
  .calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 8px;
  }
  .calendar-day-name {
    text-align: center;
    font-weight: 600;
    padding: 4px 0;
    user-select: none;
  }
  .calendar-cell {
    background: rgba(26, 70, 120, 0.7);
    min-height: 80px;
    border-radius: 8px;
    padding: 6px 8px;
    display: flex;
    flex-direction: column;
  }
  .calendar-date {
    font-weight: 700;
    font-size: 0.9rem;
    margin-bottom: 4px;
    color: #bae0ff;
  }
  .calendar-event {
    background: #2c81d7;
    margin-bottom: 3px;
    border-radius: 6px;
    padding: 4px 6px;
    font-size: 0.85rem;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    cursor: pointer;
    box-shadow: 0 1px 5px #104a82;
    transition: background-color 0.3s ease;
  }
  .calendar-event:hover {
    background-color: #4687d9;
  }
  /* Responsive & misc */
  @media (max-width: 900px) {
    main {
      flex-direction: column;
      margin: 1rem 0 2rem 0;
      max-width: 95vw;
    }
    section.form-section {
      max-width: 100%;
      margin-right: 0;
      margin-bottom: 1.5rem;
    }
    section.events-section {
      min-width: 100%;
    }
  }
  footer {
    text-align: center;
    padding: 0.8rem 1rem;
    font-size: 0.9rem;
    color: #a3c6e5;
    background: #0f3550;
    box-shadow: 0 -2px 8px rgba(0,0,0,0.4);
  }
</style>
</head>
<body>
<header>
  <h1>LINERAW</h1>
  <p class="slogan">舞點這裡找，你人到就好</p>
</header>
<main>
  <section class="form-section" aria-label="新增活動表單">
    <h2>新增街舞活動</h2>
    <form id="eventForm" novalidate>
      <label for="eventName">活動名稱 *</label>
      <input type="text" id="eventName" name="eventName" placeholder="請輸入活動名稱" required />
      
      <label for="eventDateTime">活動時間 *</label>
      <input type="datetime-local" id="eventDateTime" name="eventDateTime" required />
      
      <label for="countySelect">選擇縣市 *</label>
      <select id="countySelect" name="countySelect" required aria-describedby="countyHelp">
        <option value="">請選擇縣市</option>
        <option value="台北市">台北市</option>
        <option value="新北市">新北市</option>
        <option value="基隆市">基隆市</option>
        <option value="宜蘭縣">宜蘭縣</option>
        <option value="桃園市">桃園市</option>
        <option value="新竹市">新竹市</option>
        <option value="新竹縣">新竹縣</option>
        <option value="苗栗縣">苗栗縣</option>
        <option value="台中市">台中市</option>
        <option value="彰化縣">彰化縣</option>
        <option value="南投縣">南投縣</option>
        <option value="雲林縣">雲林縣</option>
        <option value="嘉義市">嘉義市</option>
        <option value="嘉義縣">嘉義縣</option>
        <option value="台南市">台南市</option>
        <option value="高雄市">高雄市</option>
        <option value="屏東縣">屏東縣</option>
        <option value="台東縣">台東縣</option>
        <option value="花蓮縣">花蓮縣</option>
        <option value="澎湖縣">澎湖縣</option>
        <option value="金門縣">金門縣</option>
        <option value="連江縣">連江縣</option>
      </select>
      
      <label for="locationDetail">詳細地址或地點說明 *</label>
      <input type="text" id="locationDetail" name="locationDetail" placeholder="請輸入地點(例如: 某某街舞工作室)" required />
      
      <label for="eventLink">活動連結 *</label>
      <input type="text" id="eventLink" name="eventLink" placeholder="請輸入活動相關網址" required />
      
      <label for="eventIntro">簡短介紹 *</label>
      <textarea id="eventIntro" name="eventIntro" rows="3" placeholder="簡短介紹活動內容" required></textarea>
      
      <button type="submit">新增活動</button>
    </form>
  </section>
  <section class="events-section" aria-label="活動列表與行事曆展示">
    <div class="controls" role="region" aria-label="活動控制區">
      <input type="search" id="searchInput" placeholder="搜尋活動名稱或地點" aria-label="搜尋活動" />
      <select id="sortSelect" aria-label="時間排序">
        <option value="asc" selected>時間：由近到遠</option>
        <option value="desc">時間：由遠到近</option>
      </select>
      <div class="filter-region" role="group" aria-label="依地理位置篩選">
        <button type="button" class="region-btn active" data-region="all" aria-pressed="true">全部</button>
        <button type="button" class="region-btn" data-region="north" aria-pressed="false">北部</button>
        <button type="button" class="region-btn" data-region="central" aria-pressed="false">中部</button>
        <button type="button" class="region-btn" data-region="south" aria-pressed="false">南部</button>
        <button type="button" class="region-btn" data-region="east" aria-pressed="false">東部</button>
      </div>
      <button id="viewToggleBtn" aria-label="切換行事曆與列表顯示">切換至行事曆</button>
    </div>
    <div class="events-list" id="eventsList" tabindex="0" aria-live="polite" aria-relevant="additions"></div>
    <div class="calendar-view" id="calendarView" tabindex="0" hidden aria-live="polite" aria-relevant="additions">
      <div class="calendar-header">
        <button id="prevMonthBtn" aria-label="上一個月份">&lt;</button>
        <h3 id="calendarMonthYear" aria-live="polite"></h3>
        <button id="nextMonthBtn" aria-label="下一個月份">&gt;</button>
      </div>
      <div class="calendar-grid" id="calendarGrid" role="grid" aria-readonly="true" aria-label="活動行事曆"></div>
    </div>
  </section>
</main>
<footer>
  &copy; 2024 LINERAW 街舞活動資訊
</footer>

<script>
  // Region classification by county
  const regionMap = {
    "台北市": "north",
    "新北市": "north",
    "基隆市": "north",
    "宜蘭縣": "north",
    "桃園市": "north",
    "新竹市": "north",
    "新竹縣": "north",
    "苗栗縣": "central",
    "台中市": "central",
    "彰化縣": "central",
    "南投縣": "central",
    "雲林縣": "central",
    "嘉義市": "south",
    "嘉義縣": "south",
    "台南市": "south",
    "高雄市": "south",
    "屏東縣": "south",
    "台東縣": "east",
    "花蓮縣": "east",
    "澎湖縣": "east",
    "金門縣": "other",
    "連江縣": "other"
  };

  function saveEvents(events) {
    localStorage.setItem('lineraw_events', JSON.stringify(events));
  }

  function loadEvents() {
    const eventsStr = localStorage.getItem('lineraw_events');
    if (!eventsStr) return [];
    try {
      const events = JSON.parse(eventsStr);
      // Validate format
      if (Array.isArray(events)) {
        return events.filter(e => e.eventName && e.eventDateTime && e.countySelect);
      }
      return [];
    } catch {
      return [];
    }
  }

  function formatDateTime(dateStr) {
    const dt = new Date(dateStr);
    if (isNaN(dt)) return "";
    const opts = { year: 'numeric', month: 'short', day: 'numeric', hour: '2-digit', minute: '2-digit' };
    return dt.toLocaleDateString('zh-TW', opts);
  }

  // Rendering events list
  function renderEventsList(events) {
    const container = document.getElementById('eventsList');
    if (events.length === 0) {
      container.innerHTML = '<p>目前沒有符合條件的活動。</p>';
      return;
    }
    container.innerHTML = '';
    events.forEach(ev => {
      const div = document.createElement('div');
      div.className = 'event-item';
      div.tabIndex = 0;
      const name = document.createElement('div');
      name.className = 'event-name';
      name.textContent = ev.eventName;

      const time = document.createElement('div');
      time.className = 'event-time';
      time.textContent = formatDateTime(ev.eventDateTime);

      const location = document.createElement('div');
      location.className = 'event-location';
      location.textContent = ev.countySelect + '，' + ev.locationDetail;

      const intro = document.createElement('div');
      intro.className = 'event-intro';
      intro.textContent = ev.eventIntro || '';

      div.appendChild(name);
      div.appendChild(time);
      div.appendChild(location);
      if (ev.eventIntro) div.appendChild(intro);

      if (ev.eventLink) {
        const a = document.createElement('a');
        a.className = 'event-link';
        a.href = ev.eventLink;
        a.target = "_blank";
        a.rel = "noopener";
        a.textContent = "更多資訊";
        div.appendChild(a);
      }
      container.appendChild(div);
    });
  }

  // Sorting helper: ascending or descending by datetime
  function sortEvents(events, order = 'asc') {
    return events.slice().sort((a,b) => {
      const aTime = new Date(a.eventDateTime).getTime();
      const bTime = new Date(b.eventDateTime).getTime();
      return order === 'asc' ? aTime - bTime : bTime - aTime;
    });
  }

  // Filtering events by region and search keyword
  function filterEvents(events, region = 'all', keyword = '') {
    keyword = keyword.trim().toLowerCase();
    return events.filter(ev => {
      const regionMatch = (region === 'all') || (regionMap[ev.countySelect] === region);
      if (!regionMatch) return false;
      if (!keyword) return true;
      return (ev.eventName.toLowerCase().includes(keyword) ||
              ev.locationDetail.toLowerCase().includes(keyword) ||
              ev.countySelect.toLowerCase().includes(keyword));
    });
  }

  // Setup region filter buttons toggling
  function setupRegionFilterButtons() {
    const buttons = document.querySelectorAll('.region-btn');
    buttons.forEach(btn => {
      btn.addEventListener('click', () => {
        buttons.forEach(b => { b.classList.remove('active'); b.setAttribute('aria-pressed', 'false'); });
        btn.classList.add('active');
        btn.setAttribute('aria-pressed', 'true');
        applyFiltersAndRender();
      });
    });
  }

  // Calendar view helpers
  function createCalendar(year, month, events) {
    const calendarGrid = document.getElementById('calendarGrid');
    calendarGrid.innerHTML = '';
    // Show weekday names
    const weekdays = ['日', '一', '二', '三', '四', '五', '六'];
    weekdays.forEach(day => {
      const dayName = document.createElement('div');
      dayName.className = 'calendar-day-name';
      dayName.textContent = day;
      calendarGrid.appendChild(dayName);
    });

    // First day index & days in month
    const firstDay = new Date(year, month, 1).getDay();
    const daysInMonth = new Date(year, month + 1, 0).getDate();

    // Blank cells
    for(let i=0; i<firstDay; i++) {
      const blankCell = document.createElement('div');
      blankCell.className = 'calendar-cell';
      blankCell.setAttribute('aria-hidden', 'true');
      calendarGrid.appendChild(blankCell);
    }

    // Create day cells
    for(let d=1; d<=daysInMonth; d++) {
      const cell = document.createElement('div');
      cell.className = 'calendar-cell';
      cell.setAttribute('role', 'gridcell');
      cell.setAttribute('tabindex', 0);
      // Date label
      const dateLabel = document.createElement('div');
      dateLabel.className = 'calendar-date';
      dateLabel.textContent = d;
      cell.appendChild(dateLabel);

      // Events on this day
      const dayStart = new Date(year, month, d,0,0,0).getTime();
      const dayEnd = new Date(year, month, d,23,59,59).getTime();
      
      const dayEvents = events.filter(ev => {
        const evTime = new Date(ev.eventDateTime).getTime();
        return evTime >= dayStart && evTime <= dayEnd;
      });
      dayEvents.forEach(ev => {
        const evDiv = document.createElement('div');
        evDiv.className = 'calendar-event';
        evDiv.textContent = ev.eventName;
        evDiv.title = `${formatDateTime(ev.eventDateTime)}\n${ev.countySelect}，${ev.locationDetail}`;
        evDiv.tabIndex = 0;
        evDiv.addEventListener('click', () => {
          if(ev.eventLink) window.open(ev.eventLink, '_blank', 'noopener');
        });
        evDiv.addEventListener('keypress', (e) => {
          if (e.key === 'Enter' || e.key === ' ') {
            e.preventDefault();
            if (ev.eventLink) window.open(ev.eventLink, '_blank', 'noopener');
          }
        });
        cell.appendChild(evDiv);
      });

      calendarGrid.appendChild(cell);
    }
  }

  // Update calendar header label
  function updateCalendarHeader(year, month) {
    const header = document.getElementById('calendarMonthYear');
    const monthNames = ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'];
    header.textContent = `${year}年 ${monthNames[month]}`;
  }

  // Main internal state
  let events = [];
  let currentRegion = 'all';
  let currentSort = 'asc';
  let currentKeyword = '';
  let calendarYear;
  let calendarMonth;

  // Apply filters, sort and render
  function applyFiltersAndRender() {
    currentKeyword = document.getElementById('searchInput').value;
    const filtered = filterEvents(events, currentRegion, currentKeyword);
    const sorted = sortEvents(filtered, currentSort);
    if (document.getElementById('calendarView').hidden) {
      renderEventsList(sorted);
    } else {
      createCalendar(calendarYear, calendarMonth, sorted);
      updateCalendarHeader(calendarYear, calendarMonth);
    }
  }

  // Form submission handler
  document.getElementById('eventForm').addEventListener('submit', e => {
    e.preventDefault();
    const form = e.target;
    const newEvent = {
      eventName: form.eventName.value.trim(),
      eventDateTime: form.eventDateTime.value,
      countySelect: form.countySelect.value,
      locationDetail: form.locationDetail.value.trim(),
      eventLink: form.eventLink.value.trim(),
      eventIntro: form.eventIntro.value.trim()
    };
    if (!newEvent.eventName || !newEvent.eventDateTime || !newEvent.countySelect || !newEvent.locationDetail || !newEvent.eventLink || !newEvent.eventIntro) {
      alert('請填寫所有必填欄位！');
      return;
    }
    events.push(newEvent);
    saveEvents(events);
    form.reset();
    alert('活動已新增！');
    applyFiltersAndRender();
  });

  // Search input handler
  document.getElementById('searchInput').addEventListener('input', () => {
    applyFiltersAndRender();
  });

  // Sorting selector handler
  document.getElementById('sortSelect').addEventListener('change', e => {
    currentSort = e.target.value;
    applyFiltersAndRender();
  });

  // Region filter buttons
  setupRegionFilterButtons();
  // Initially set currentRegion from active button
  currentRegion = document.querySelector('.region-btn.active').dataset.region;

  // View toggle button
  const viewToggleBtn = document.getElementById('viewToggleBtn');
  viewToggleBtn.addEventListener('click', () => {
    const listView = document.getElementById('eventsList');
    const calendarView = document.getElementById('calendarView');
    if (listView.hidden) {
      // Switch to list
      listView.hidden = false;
      calendarView.hidden = true;
      viewToggleBtn.textContent = '切換至行事曆';
      viewToggleBtn.setAttribute('aria-label', '切換行事曆與列表顯示');
    } else {
      // Switch to calendar
      // Set to current month/year
      const now = new Date();
      calendarYear = now.getFullYear();
      calendarMonth = now.getMonth();
      createCalendar(calendarYear, calendarMonth, filterEvents(events, currentRegion, currentKeyword));
      updateCalendarHeader(calendarYear, calendarMonth);
      listView.hidden = true;
      calendarView.hidden = false;
      viewToggleBtn.textContent = '切換至列表';
      viewToggleBtn.setAttribute('aria-label', '切換列表與行事曆顯示');
    }
  });

  // Calendar month navigation
  document.getElementById('prevMonthBtn').addEventListener('click', () => {
    calendarMonth--;
    if (calendarMonth < 0) {
      calendarMonth = 11;
      calendarYear--;
    }
    createCalendar(calendarYear, calendarMonth, filterEvents(events, currentRegion, currentKeyword));
    updateCalendarHeader(calendarYear, calendarMonth);
  });
  document.getElementById('nextMonthBtn').addEventListener('click', () => {
    calendarMonth++;
    if (calendarMonth > 11) {
      calendarMonth = 0;
      calendarYear++;
    }
    createCalendar(calendarYear, calendarMonth, filterEvents(events, currentRegion, currentKeyword));
    updateCalendarHeader(calendarYear, calendarMonth);
  });

  // Region button event listeners update currentRegion
  document.querySelectorAll('.region-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      currentRegion = btn.dataset.region;
      applyFiltersAndRender();
    });
  });

  // Load events on page load
  window.addEventListener('load', () => {
    events = loadEvents();
    applyFiltersAndRender();
    // Initialize calendar to current month
    const now = new Date();
    calendarYear = now.getFullYear();
    calendarMonth = now.getMonth();
  });
</script>
</body>
</html>


