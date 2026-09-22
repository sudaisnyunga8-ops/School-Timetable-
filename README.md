# School-Timetable-
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sudais's Cyber Timetable</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            cyber: { bg: '#0c0a1d', card: '#15122c', cardHover: '#1e1a3f', purple: '#8b5cf6', neonPurple: '#a855f7', cyan: '#06b6d4', pink: '#ec4899', darkBorder: 'rgba(255, 255, 255, 0.08)' }
          }
        }
      }
    }
  </script>
  <style>
    body { background-color: #0c0a1d; color: #f8fafc; font-family: system-ui, -apple-system, sans-serif; }
    .glass-header { background: rgba(12, 10, 29, 0.85); backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px); border-bottom: 1px solid rgba(255, 255, 255, 0.08); }
    .cyber-card { background: linear-gradient(135deg, rgba(21, 18, 44, 0.9), rgba(13, 11, 31, 0.95)); border: 1px solid rgba(255, 255, 255, 0.06); box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4); }
    .cyber-card:hover { border-color: rgba(139, 92, 246, 0.3); }
    .neon-glow { box-shadow: 0 0 20px rgba(139, 92, 246, 0.25); }
    .pulse-dot { width: 8px; height: 8px; background-color: #06b6d4; border-radius: 50%; box-shadow: 0 0 10px #06b6d4; animation: pulse 2s infinite; }
    @keyframes pulse { 0% { transform: scale(0.95); opacity: 0.8; } 50% { transform: scale(1.25); opacity: 1; } 100% { transform: scale(0.95); opacity: 0.8; } }
    /* Hide scrollbar for Chrome, Safari and Opera */
    .no-scrollbar::-webkit-scrollbar { display: none; }
    /* Hide scrollbar for IE, Edge and Firefox */
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
  </style>
</head>
<body class="min-h-screen pb-24">

  <!-- Top Sticky Header -->
  <header class="glass-header sticky top-0 z-50 px-4 py-3 flex flex-col gap-2">
    <div class="flex items-center justify-between">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-purple-600 to-cyan-400 p-0.5 flex items-center justify-center neon-glow">
          <div class="w-full h-full bg-cyber-bg rounded-[10px] flex items-center justify-center font-black text-cyan-400 text-sm">SN</div>
        </div>
        <div>
          <h1 class="text-sm font-bold tracking-wide text-white">Sudais Nyunga</h1>
          <p class="text-xs text-slate-400">S4 • 08:50 - 15:15</p>
        </div>
      </div>
      <div class="flex items-center gap-2 bg-purple-950/40 border border-purple-500/30 px-3 py-1.5 rounded-full">
        <span class="pulse-dot"></span>
        <span id="live-status" class="text-xs font-medium text-purple-200">School Active</span>
      </div>
    </div>

    <!-- Live Countdown Banner -->
    <div class="cyber-card rounded-xl p-3 flex items-center justify-between border border-purple-500/20 bg-gradient-to-r from-purple-900/20 to-cyan-900/20">
      <div class="flex flex-col">
        <span class="text-[10px] font-bold uppercase tracking-wider text-cyan-400">Next Up / Status</span>
        <span id="next-class-title" class="text-xs font-semibold text-white">Loading schedule...</span>
      </div>
      <div class="text-right">
        <span id="countdown-timer" class="text-sm font-mono font-bold text-purple-300">--:--:--</span>
      </div>
    </div>
  </header>

  <!-- Main Content Container -->
  <main class="max-w-md mx-auto px-4 pt-4">

    <!-- Day Selector Tabs -->
    <div class="flex gap-2 overflow-x-auto no-scrollbar pb-2 mb-4">
      <button onclick="setDay('Monday')" id="btn-Monday" class="day-btn px-4 py-2 rounded-xl text-xs font-semibold transition-all whitespace-nowrap bg-purple-600 text-white shadow-lg shadow-purple-600/30">Monday</button>
      <button onclick="setDay('Tuesday')" id="btn-Tuesday" class="day-btn px-4 py-2 rounded-xl text-xs font-semibold transition-all whitespace-nowrap bg-cyber-card text-slate-400 border border-slate-800">Tuesday</button>
      <button onclick="setDay('Wednesday')" id="btn-Wednesday" class="day-btn px-4 py-2 rounded-xl text-xs font-semibold transition-all whitespace-nowrap bg-cyber-card text-slate-400 border border-slate-800">Wednesday</button>
      <button onclick="setDay('Thursday')" id="btn-Thursday" class="day-btn px-4 py-2 rounded-xl text-xs font-semibold transition-all whitespace-nowrap bg-cyber-card text-slate-400 border border-slate-800">Thursday</button>
      <button onclick="setDay('Friday')" id="btn-Friday" class="day-btn px-4 py-2 rounded-xl text-xs font-semibold transition-all whitespace-nowrap bg-cyber-card text-slate-400 border border-slate-800">Friday</button>
    </div>

    <!-- Active Day Header Display -->
    <div class="flex items-center justify-between mb-3 px-1">
      <h2 id="current-day-label" class="text-base font-bold text-slate-200">Monday Schedule</h2>
      <span id="class-count" class="text-xs text-slate-400">0 classes</span>
    </div>

    <!-- Timetable Cards List -->
    <div id="timetable-list" class="flex flex-col gap-3">
      <!-- Injected via JavaScript -->
    </div>

  </main>

  <!-- Floating Bottom Navigation -->
  <nav class="fixed bottom-4 left-4 right-4 max-w-md mx-auto glass-header rounded-2xl p-2 flex items-center justify-around border border-white/10 shadow-2xl z-50">
    <button onclick="switchTab('timetable')" class="flex flex-col items-center gap-1 text-cyan-400 py-1 px-4">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect width="18" height="18" x="3" y="4" rx="2" ry="2"/><line x1="16" x2="16" y1="2" y2="6"/><line x1="8" x2="8" y1="2" y2="6"/><line x1="3" x2="21" y1="10" y2="10"/></svg>
      <span class="text-[10px] font-medium">Timetable</span>
    </button>
    <button onclick="switchTab('bells')" class="flex flex-col items-center gap-1 text-slate-400 hover:text-white py-1 px-4 transition-colors">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M12 2v2m4.93 1.07l-1.41 1.41M20 12h2m-2.07 4.93l1.41 1.41M12 22v-2m-4.93-1.07l1.41-1.41M2 12H0m2.07-4.93L.66 5.66"/></svg>
      <span class="text-[10px] font-medium">Bell Times</span>
    </button>
  </nav>

  <script>
    // Full Custom Schedule Data (Math -> Mr McLarty everyday, Period 7 -> Mr Fulton Mon-Thu, Mr McGimpsy Fri)
    const scheduleData = {
      Monday: [
        { start: '08:50', end: '09:40', name: 'Administration', teacher: 'Mr McDermott', room: 'F24', type: 'class' },
        { start: '09:40', end: '10:25', name: 'PE Core 5–14', teacher: 'Mr McGimpsy', room: 'P/E', type: 'class' },
        { start: '10:25', end: '11:10', name: 'Modern Studies', teacher: 'Mr Kelly', room: 'S23', type: 'class' },
        { start: '11:10', end: '11:25', name: 'Morning Break', teacher: 'Break', room: 'Cafeteria', type: 'break' },
        { start: '11:25', end: '12:15', name: 'Mathematics', teacher: 'Mr McLarty', room: 'F1', type: 'class' },
        { start: '12:15', end: '13:05', name: 'RE Core 5–14', teacher: 'Mr Mackay', room: 'S13', type: 'class' },
        { start: '13:05', end: '13:50', name: 'Lunch', teacher: 'Break', room: 'Dining Hall', type: 'break' },
        { start: '13:50', end: '14:35', name: 'Science', teacher: 'Dr Smith', room: 'Sc4', type: 'class' },
        { start: '14:35', end: '15:15', name: 'English', teacher: 'Mr Fulton', room: 'E2', type: 'class' }
      ],
      Tuesday: [
        { start: '08:50', end: '09:40', name: 'English', teacher: 'Mr Fulton', room: 'E2', type: 'class' },
        { start: '09:40', end: '10:25', name: 'Mathematics', teacher: 'Mr McLarty', room: 'F1', type: 'class' },
        { start: '10:25', end: '11:10', name: 'History', teacher: 'Ms Vance', room: 'H1', type: 'class' },
        { start: '11:10', end: '11:25', name: 'Morning Break', teacher: 'Break', room: 'Cafeteria', type: 'break' },
        { start: '11:25', end: '12:15', name: 'Chemistry', teacher: 'Dr Brown', room: 'Sc1', type: 'class' },
        { start: '12:15', end: '13:05', name: 'Computing', teacher: 'Mr Gates', room: 'IT1', type: 'class' },
        { start: '13:05', end: '13:50', name: 'Lunch', teacher: 'Break', room: 'Dining Hall', type: 'break' },
        { start: '13:50', end: '14:35', name: 'Art & Design', teacher: 'Ms Artie', room: 'A1', type: 'class' },
        { start: '14:35', end: '15:15', name: 'Period 7 Study', teacher: 'Mr Fulton', room: 'S10', type: 'class' }
      ],
      Wednesday: [
        { start: '08:50', end: '09:40', name: 'Administration', teacher: 'Mr McDermott', room: 'F24', type: 'class' },
        { start: '09:40', end: '10:25', name: 'PE Core 5–14', teacher: 'Mr McGimpsy', room: 'P/E', type: 'class' },
        { start: '10:25', end: '11:10', name: 'Modern Studies', teacher: 'Mr Kelly', room: 'S23', type: 'class' },
        { start: '11:10', end: '11:25', name: 'Morning Break', teacher: 'Break', room: 'Cafeteria', type: 'break' },
        { start: '11:25', end: '12:15', name: 'Mathematics', teacher: 'Mr McLarty', room: 'F1', type: 'class' },
        { start: '12:15', end: '13:05', name: 'RE Core 5–14', teacher: 'Mr Mackay', room: 'S13', type: 'class' },
        { start: '13:05', end: '13:50', name: 'Lunch', teacher: 'Break', room: 'Dining Hall', type: 'break' },
        { start: '13:50', end: '14:35', name: 'Physics', teacher: 'Mr Newton', room: 'Sc2', type: 'class' },
        { start: '14:35', end: '15:15', name: 'Period 7 Extra', teacher: 'Mr Fulton', room: 'F2', type: 'class' }
      ],
      Thursday: [
        { start: '08:50', end: '09:40', name: 'Geography', teacher: 'Ms Globe', room: 'G4', type: 'class' },
        { start: '09:40', end: '10:25', name: 'Mathematics', teacher: 'Mr McLarty', room: 'F1', type: 'class' },
        { start: '10:25', end: '11:10', name: 'Biology', teacher: 'Dr Leaf', room: 'Sc3', type: 'class' },
        { start: '11:10', end: '11:25', name: 'Morning Break', teacher: 'Break', room: 'Cafeteria', type: 'break' },
        { start: '11:25', end: '12:15', name: 'English', teacher: 'Mr Fulton', room: 'E2', type: 'class' },
        { start: '12:15', end: '13:05', name: 'Music', teacher: 'Mr Mozart', room: 'M1', type: 'class' },
        { start: '13:05', end: '13:50', name: 'Lunch', teacher: 'Break', room: 'Dining Hall', type: 'break' },
        { start: '13:50', end: '14:35', name: 'Modern Studies', teacher: 'Mr Kelly', room: 'S23', type: 'class' },
        { start: '14:35', end: '15:15', name: 'Period 7 Tutor', teacher: 'Mr Fulton', room: 'T1', type: 'class' }
      ],
      Friday: [
        { start: '08:50', end: '09:40', name: 'Mathematics', teacher: 'Mr McLarty', room: 'F1', type: 'class' },
        { start: '09:40', end: '10:25', name: 'English', teacher: 'Mr Fulton', room: 'E2', type: 'class' },
        { start: '10:25', end: '11:10', name: 'Drama', teacher: 'Ms Stage', room: 'D1', type: 'class' },
        { start: '11:10', end: '11:25', name: 'Morning Break', teacher: 'Break', room: 'Cafeteria', type: 'break' },
        { start: '11:25', end: '12:15', name: 'Computing', teacher: 'Mr Gates', room: 'IT1', type: 'class' },
        { start: '12:15', end: '13:05', name: 'Modern Studies', teacher: 'Mr Kelly', room: 'S23', type: 'class' },
        { start: '13:05', end: '13:50', name: 'Lunch', teacher: 'Break', room: 'Dining Hall', type: 'break' },
        { start: '13:50', end: '14:35', name: 'Science', teacher: 'Dr Smith', room: 'Sc4', type: 'class' },
        { start: '14:35', end: '15:15', name: 'PE Activity', teacher: 'Mr McGimpsy', room: 'P/E', type: 'class' }
      ]
    };

    let activeDay = 'Monday';

    // Auto-select today's day of the week on load
    const daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const todayName = daysOfWeek[new Date().getDay()];
    if (scheduleData[todayName]) {
      activeDay = todayName;
    }

    function setDay(day) {
      activeDay = day;
      document.querySelectorAll('.day-btn').forEach(btn => {
        if(btn.id === `btn-${day}`) {
          btn.className = "day-btn px-4 py-2 rounded-xl text-xs font-semibold transition-all whitespace-nowrap bg-purple-600 text-white shadow-lg shadow-purple-600/30";
        } else {
          btn.className = "day-btn px-4 py-2 rounded-xl text-xs font-semibold transition-all whitespace-nowrap bg-cyber-card text-slate-400 border border-slate-800";
        }
      });
      renderTimetable();
    }

    function renderTimetable() {
      const listContainer = document.getElementById('timetable-list');
      const dayLabel = document.getElementById('current-day-label');
      const classCount = document.getElementById('class-count');
      
      dayLabel.innerText = `${activeDay} Schedule`;
      const classes = scheduleData[activeDay];
      classCount.innerText = `${classes.filter(c => c.type === 'class').length} classes`;

      listContainer.innerHTML = '';

      classes.forEach((item, index) => {
        const isBreak = item.type === 'break';
        const card = document.createElement('div');
        card.className = `cyber-card rounded-2xl p-4 flex items-center justify-between transition-all ${isBreak ? 'border-amber-500/30 bg-amber-950/10' : ''}`;
        
        card.innerHTML = `
          <div class="flex items-center gap-3">
            <div class="w-14 py-2 rounded-xl ${isBreak ? 'bg-amber-500/20 text-amber-300 border border-amber-500/30' : 'bg-purple-950/60 text-purple-300 border border-purple-500/20'} flex flex-col items-center justify-center font-mono text-xs font-bold">
              <span>${item.start}</span>
            </div>
            <div>
              <div class="flex items-center gap-2">
                <h3 class="text-sm font-bold text-white">${item.name}</h3>
                ${isBreak ? '<span class="text-[10px] bg-amber-500/20 text-amber-300 px-2 py-0.5 rounded-full font-bold">BREAK</span>' : ''}
              </div>
              <p class="text-xs text-slate-400 mt-0.5">${item.teacher} • <span class="text-cyan-400">${item.room}</span></p>
            </div>
          </div>
          <div class="text-right">
            <span class="text-xs font-mono text-slate-500">${item.end}</span>
          </div>
        `;
        listContainer.appendChild(card);
      });
    }

    // Live Countdown and Status Engine
    function updateCountdown() {
      const now = new Date();
      const currentDayStr = daysOfWeek[now.getDay()];
      const currentTimeMins = now.getHours() * 60 + now.getMinutes();
      const currentSecs = now.getSeconds();

      const titleEl = document.getElementById('next-class-title');
      const timerEl = document.getElementById('countdown-timer');
      const statusEl = document.getElementById('live-status');

      if (!scheduleData[currentDayStr] || currentDayStr === 'Saturday' || currentDayStr === 'Sunday') {
        statusEl.innerText = "Weekend / No School";
        titleEl.innerText = "Enjoy your weekend!";
        timerEl.innerText = "CLOSED";
        return;
      }

      const dayClasses = scheduleData[currentDayStr];
      let nextClass = null;

      for (let cls of dayClasses) {
        const [sh, sm] = cls.start.split(':').map(Number);
        const startMins = sh * 60 + sm;
        if (startMins > currentTimeMins) {
          nextClass = cls;
          break;
        }
      }

      if (nextClass) {
        statusEl.innerText = "School Active";
        titleEl.innerText = `Next: ${nextClass.name} (${nextClass.room})`;

        const [sh, sm] = nextClass.start.split(':').map(Number);
        const targetTotalSecs = (sh * 3600 + sm * 60);
        const currentTotalSecs = (now.getHours() * 3600 + now.getMinutes() * 60 + now.getSeconds());
        let diffSecs = targetTotalSecs - currentTotalSecs;

        const h = Math.floor(diffSecs / 3600);
        const m = Math.floor((diffSecs % 3600) / 60);
        const s = diffSecs % 60;

        timerEl.innerText = `${h > 0 ? h + 'h ' : ''}${m.toString().padStart(2, '0')}m ${s.toString().padStart(2, '0')}s`;
      } else {
        statusEl.innerText = "School Day Ended";
        titleEl.innerText = "All Classes Finished";
        timerEl.innerText = "00:00:00";
      }
    }

    function switchTab(tab) {
      if(tab === 'timetable') {
        setDay(activeDay);
      } else {
        const listContainer = document.getElementById('timetable-list');
        document.getElementById('current-day-label').innerText = "Bell Times Schedule";
        document.getElementById('class-count').innerText = "Standard Bells";
        listContainer.innerHTML = `
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Warning Bell</span><span class="font-mono text-cyan-400">08:45 AM</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Period 1</span><span class="font-mono text-cyan-400">08:50 - 09:40</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Period 2</span><span class="font-mono text-cyan-400">09:40 - 10:25</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Period 3</span><span class="font-mono text-cyan-400">10:25 - 11:10</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-amber-400">Morning Break</span><span class="font-mono text-amber-300">11:10 - 11:25</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Period 4</span><span class="font-mono text-cyan-400">11:25 - 12:15</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Period 5</span><span class="font-mono text-cyan-400">12:15 - 13:05</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-amber-400">Lunch Break</span><span class="font-mono text-amber-300">13:05 - 13:50</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Period 6</span><span class="font-mono text-cyan-400">13:50 - 14:35</span></div>
          <div class="cyber-card rounded-2xl p-4 flex justify-between items-center"><span class="text-sm font-bold text-white">Period 7</span><span class="font-mono text-cyan-400">14:35 - 15:15</span></div>
        `;
      }
    }

    // Initialize app
    setDay(activeDay);
    setInterval(updateCountdown, 1000);
    updateCountdown();
  </script>
</body>
</html>
