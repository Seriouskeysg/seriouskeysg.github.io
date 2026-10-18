<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>BlackPanther Barbershop</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d0d0d;
    --panel: #161616;
    --line: #2a2a2a;
    --text: #f2f2f2;
    --muted: #9a9a9a;
    --accent: #d4af37;
    --accent-dark: #a8861f;
    --danger: #c0392b;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Inter', system-ui, sans-serif;
    line-height: 1.6;
  }
  h1, h2, h3 { font-family: 'Bebas Neue', Impact, sans-serif; letter-spacing: 1px; font-weight: 400; }
  a { color: var(--accent); text-decoration: none; }
  a:hover { text-decoration: underline; }
  .container { max-width: 1040px; margin: 0 auto; padding: 0 20px; }

  /* Nav */
  nav {
    position: sticky; top: 0; z-index: 10;
    background: rgba(13,13,13,0.95);
    border-bottom: 1px solid var(--line);
    backdrop-filter: blur(6px);
  }
  nav .container { display: flex; align-items: center; justify-content: space-between; height: 64px; }
  .brand { font-family: 'Bebas Neue', Impact, sans-serif; font-size: 1.6rem; color: var(--text); letter-spacing: 2px; }
  .brand span { color: var(--accent); }
  nav ul { list-style: none; display: flex; gap: 22px; }
  nav a { color: var(--muted); font-size: 0.9rem; }
  nav a:hover { color: var(--accent); text-decoration: none; }
  .btn {
    display: inline-block; background: var(--accent); color: #0d0d0d;
    padding: 12px 26px; font-weight: 600; border: none; cursor: pointer;
    font-family: inherit; font-size: 0.95rem; letter-spacing: 0.5px;
  }
  .btn:hover { background: var(--accent-dark); text-decoration: none; }
  .btn.ghost { background: transparent; color: var(--accent); border: 1px solid var(--accent); }
  .btn.ghost:hover { background: rgba(212,175,55,0.1); }

  /* Hero */
  .hero {
    padding: 120px 0 100px;
    text-align: center;
    background:
      radial-gradient(ellipse at top, rgba(212,175,55,0.12), transparent 60%),
      var(--bg);
    border-bottom: 1px solid var(--line);
  }
  .hero h1 { font-size: clamp(3.2rem, 9vw, 6rem); line-height: 0.95; }
  .hero h1 span { color: var(--accent); }
  .hero p { color: var(--muted); max-width: 520px; margin: 22px auto 34px; font-size: 1.05rem; }
  .rating { color: var(--accent); font-weight: 600; margin-bottom: 14px; font-size: 0.95rem; }

  section { padding: 84px 0; border-bottom: 1px solid var(--line); }
  section:last-of-type { border-bottom: none; }
  .section-title { font-size: 2.6rem; margin-bottom: 8px; }
  .section-sub { color: var(--muted); margin-bottom: 40px; }

  /* Info grid */
  .info-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(230px, 1fr)); gap: 20px; }
  .card { background: var(--panel); border: 1px solid var(--line); padding: 28px; }
  .card h3 { color: var(--accent); font-size: 1.4rem; margin-bottom: 10px; }
  .card p, .card li { color: var(--muted); font-size: 0.95rem; }
  .card ul { list-style: none; }
  .card li { padding: 6px 0; border-bottom: 1px dashed var(--line); display: flex; justify-content: space-between; gap: 12px; }
  .card li:last-child { border-bottom: none; }
  .card li b { color: var(--text); font-weight: 500; }

  /* Booking */
  .booking { background: var(--panel); border: 1px solid var(--line); padding: 36px; }
  .steps { display: flex; gap: 10px; margin-bottom: 30px; flex-wrap: wrap; }
  .step-pill {
    padding: 6px 14px; border: 1px solid var(--line); color: var(--muted);
    font-size: 0.85rem; border-radius: 999px;
  }
  .step-pill.active { border-color: var(--accent); color: var(--accent); }
  .step-pill.done { color: var(--text); }
  .panel { display: none; }
  .panel.active { display: block; }
  .panel h3 { font-size: 1.6rem; margin-bottom: 18px; }

  .options { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 14px; }
  .option {
    background: var(--bg); border: 1px solid var(--line); padding: 18px;
    cursor: pointer; transition: border-color .15s, transform .15s;
  }
  .option:hover { border-color: var(--accent-dark); transform: translateY(-2px); }
  .option.selected { border-color: var(--accent); box-shadow: inset 0 0 0 1px var(--accent); }
  .option strong { display: block; font-size: 1rem; margin-bottom: 4px; }
  .option small { color: var(--muted); }
  .option .price { color: var(--accent); font-weight: 600; margin-top: 8px; display: block; }

  .slots { display: grid; grid-template-columns: repeat(auto-fill, minmax(110px, 1fr)); gap: 10px; margin-top: 10px; }
  .slot {
    background: var(--bg); border: 1px solid var(--line); padding: 10px;
    text-align: center; cursor: pointer; font-size: 0.92rem; color: var(--text);
    font-family: inherit;
  }
  .slot:hover:not(:disabled) { border-color: var(--accent); }
  .slot.selected { background: var(--accent); color: #0d0d0d; border-color: var(--accent); }
  .slot:disabled { opacity: .3; cursor: not-allowed; text-decoration: line-through; }

  .date-row { display: flex; gap: 10px; overflow-x: auto; padding-bottom: 6px; margin-bottom: 18px; }
  .date-chip {
    flex: 0 0 auto; background: var(--bg); border: 1px solid var(--line);
    padding: 10px 14px; text-align: center; cursor: pointer; min-width: 76px;
    font-family: inherit; color: var(--text);
  }
  .date-chip small { display: block; color: var(--muted); font-size: 0.75rem; }
  .date-chip strong { font-size: 1.1rem; }
  .date-chip.selected { border-color: var(--accent); color: var(--accent); }
  .date-chip:disabled { opacity: .35; cursor: not-allowed; }

  .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-grid .full { grid-column: 1 / -1; }
  label { display: block; font-size: 0.85rem; color: var(--muted); margin-bottom: 6px; }
  input, textarea {
    width: 100%; background: var(--bg); border: 1px solid var(--line); color: var(--text);
    padding: 12px; font-family: inherit; font-size: 0.95rem;
  }
  input:focus, textarea:focus { outline: none; border-color: var(--accent); }
  textarea { min-height: 80px; resize: vertical; }

  .actions { display: flex; justify-content: space-between; margin-top: 26px; gap: 12px; }
  .summary { background: var(--bg); border: 1px solid var(--line); padding: 18px; margin-bottom: 20px; }
  .summary div { display: flex; justify-content: space-between; padding: 7px 0; border-bottom: 1px dashed var(--line); font-size: 0.95rem; }
  .summary div:last-child { border-bottom: none; }
  .summary span:first-child { color: var(--muted); }
  .error { color: var(--danger); font-size: 0.88rem; margin-top: 10px; min-height: 1.2em; }

  .confirm { text-align: center; padding: 30px 0; }
  .confirm .tick {
    width: 64px; height: 64px; border-radius: 50%; background: var(--accent); color: #0d0d0d;
    display: inline-flex; align-items: center; justify-content: center; font-size: 2rem; margin-bottom: 18px;
  }
  .confirm p { color: var(--muted); margin: 10px 0 22px; }

  /* Reviews / contact / social */
  .contact-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 20px; }
  .contact-item .label { color: var(--muted); font-size: 0.8rem; text-transform: uppercase; letter-spacing: 1px; }
  .contact-item .value { font-size: 1.1rem; margin-top: 4px; }
  .social { display: flex; gap: 12px; margin-top: 28px; flex-wrap: wrap; }

  footer { text-align: center; padding: 36px 0; color: var(--muted); font-size: 0.85rem; border-top: 1px solid var(--line); }

  @media (max-width: 700px) {
    nav ul { display: none; }
    .form-grid { grid-template-columns: 1fr; }
    .booking { padding: 22px; }
    section { padding: 60px 0; }
    .section-title { font-size: 2.1rem; }
  }
</style>
</head>
<body>

<nav>
  <div class="container">
    <a href="#top" class="brand">BLACK<span>PANTHER</span></a>
    <ul>
      <li><a href="#about">About</a></li>
      <li><a href="#services">Services</a></li>
      <li><a href="#book">Book</a></li>
      <li><a href="#visit">Visit</a></li>
    </ul>
    <a href="#book" class="btn">Book Now</a>
  </div>
</nav>

<header class="hero" id="top">
  <div class="container">
    <div class="rating">★★★★½ &nbsp;4.5 from Google reviews</div>
    <h1>Sharp cuts.<br><span>Every visit.</span></h1>
    <p>Barbershop in Johor Bahru, Malaysia. Walk in or book your chair ahead of time.</p>
    <a href="#book" class="btn">Book an Appointment</a>
  </div>
</header>

<section id="about">
  <div class="container">
    <h2 class="section-title">About the Shop</h2>
    <p class="section-sub">BlackPanther Barbershop serves Johor Bahru with precise fades, clean lines and a relaxed chair.</p>
    <div class="info-grid">
      <div class="card">
        <h3>Rated Well</h3>
        <p>Averages 4.5 stars across Google reviews from local clients.</p>
      </div>
      <div class="card">
        <h3>Find Us</h3>
        <p>Batu 17, Kampung Tenang<br>81800 Johor Bahru<br>Johor Darul Ta'zim, Malaysia</p>
      </div>
      <div class="card">
        <h3>Opening Hours</h3>
        <ul>
        <li><span>Monday</span> <b>10:00 – 23:00</b></li>
        <li><span>Tuesday</span> <b>10:00 – 23:00</b></li>
        <li><span>Wednesday</span> <b>10:00 – 23:00</b></li>
        <li><span>Thursday</span> <b>10:00 – 23:00</b></li>
        <li><span>Friday</span> <b>15:00 – 23:00</b></li>
        <li><span>Saturday</span> <b>10:00 – 23:00</b></li>
        <li><span>Sunday</span> <b>10:00 – 23:00</b></li>
        </ul>
      </div>
    </div>
  </div>
</section>

<section id="services">
  <div class="container">
    <h2 class="section-title">Services</h2>
    <p class="section-sub">Every great look starts with the right service. Explore our curated grooming offerings and let our skilled barbers craft a style tailored to you.</p>
    <div class="info-grid">
      <div class="card">
        <h3>Haircut</h3>
        <p>Classic cut, tapered or scissor work, finished with a neck line.</p>
        <p style="color: var(--accent); font-weight:600; margin-top:12px;">RM 25</p>
      </div>
      <div class="card">
        <h3>Fade</h3>
        <p>Low, mid or high fade blended cleanly, with a line-up included.</p>
        <p style="color: var(--accent); font-weight:600; margin-top:12px;">RM 30</p>
      </div>
      <div class="card">
        <h3>Beard Trim</h3>
        <p>Shape and detail, with hot towel finish.</p>
        <p style="color: var(--accent); font-weight:600; margin-top:12px;">RM 15</p>
      </div>
      <div class="card">
        <h3>Haircut + Beard</h3>
        <p>Full cut and beard grooming in one visit.</p>
        <p style="color: var(--accent); font-weight:600; margin-top:12px;">RM 38</p>
      </div>
    </div>
  </div>
</section>

<section id="book">
  <div class="container">
    <h2 class="section-title">Book a Chair</h2>
    <p class="section-sub">Pick a service, a barber, a date and a time. Booking is saved to this browser.</p>

    <div class="booking">
      <div class="steps">
        <span class="step-pill active" data-step="1">1. Service</span>
        <span class="step-pill" data-step="2">2. Barber</span>
        <span class="step-pill" data-step="3">3. Date &amp; Time</span>
        <span class="step-pill" data-step="4">4. Your Details</span>
      </div>

      <!-- Step 1: Service -->
      <div class="panel active" id="panel-1">
        <h3>Choose a service</h3>
        <div class="options" id="service-options"></div>
        <div class="actions">
          <span></span>
          <button class="btn" data-next>Next</button>
        </div>
      </div>

      <!-- Step 2: Barber -->
      <div class="panel" id="panel-2">
        <h3>Choose your barber</h3>
        <div class="options" id="barber-options"></div>
        <div class="actions">
          <button class="btn ghost" data-back>Back</button>
          <button class="btn" data-next>Next</button>
        </div>
      </div>

      <!-- Step 3: Date & time -->
      <div class="panel" id="panel-3">
        <h3>Pick a date and time</h3>
        <div class="date-row" id="date-row"></div>
        <div class="slots" id="slot-grid"></div>
        <div class="actions">
          <button class="btn ghost" data-back>Back</button>
          <button class="btn" data-next>Next</button>
        </div>
      </div>

      <!-- Step 4: Details -->
      <div class="panel" id="panel-4">
        <h3>Your details</h3>
        <div class="form-grid">
          <div>
            <label for="name">Full name</label>
            <input id="name" type="text" placeholder="e.g. Ahmad Irfan">
          </div>
          <div>
            <label for="phone">Phone (WhatsApp)</label>
            <input id="phone" type="tel" placeholder="+60 12-345 6789">
          </div>
          <div class="full">
            <label for="notes">Notes for your barber (optional)</label>
            <textarea id="notes" placeholder="e.g. Skin fade, keep the top longer"></textarea>
          </div>
        </div>
        <div class="error" id="form-error"></div>
        <div class="actions">
          <button class="btn ghost" data-back>Back</button>
          <button class="btn" id="confirm-btn">Confirm Booking</button>
        </div>
      </div>

      <!-- Confirmation -->
      <div class="panel" id="panel-done">
        <div class="confirm">
          <div class="tick">✓</div>
          <h3>You're booked</h3>
          <p>We've saved your appointment. Please arrive a few minutes early.</p>
          <div class="summary" id="final-summary" style="text-align:left;"></div>
          <button class="btn ghost" id="new-booking">Make another booking</button>
        </div>
      </div>
    </div>
  </div>
</section>

<section id="visit">
  <div class="container">
    <h2 class="section-title">Visit Us</h2>
    <p class="section-sub">Walk in or call ahead. Find us on the map or reach out directly.</p>
    <div class="contact-grid">
      <div class="contact-item">
        <div class="label">Address</div>
        <div class="value">Batu 17, Kampung Tenang<br>81800 Johor Bahru, Johor, Malaysia</div>
      </div>
      <div class="contact-item">
        <div class="label">Phone</div>
        <div class="value"><a href="tel:‪+601119986186‬">‪+60 11‑1998 6186‬</a></div>
      </div>
      <div class="contact-item">
        <div class="label">Hours</div>
        <div class="value">Open daily from 10:00-23:00 (Friday 15:00-23:00) </div>
      </div>
    </div>
    <div class="social">
      <a class="btn ghost" href="[https://www.instagram.com/blackpanther_barbershops](https://www.tiktok.com/@boy.blackpanther" target="_blank" rel="noopener">Instagram</a>
      <a class="btn ghost" href="[https://www.tiktok.com/@bpsbarbershop](https://www.instagram.com/boy.blackpanther01" target="_blank" rel="noopener">TikTok</a>
      <a class="btn ghost" href="https://www.google.com/search?q=black+panther+barbershop+johor+bahru" target="_blank" rel="noopener">Reviews on Google</a>
    </div>
  </div>
</section>

<footer>
  <div class="container">
    © 2026 BlackPanther Barbershop · Batu 17, Kampung Tenang, Johor Bahru, Malaysia
    · Supported by HAAQ Pte Ltd, Singapore
  </div>
</footer>

<script>
(function () {
  // ---------- Config ----------
  const SERVICES = [
    { id: 'haircut',  name: 'Haircut',         desc: 'Classic cut and neck line',   price: 25, mins: 30 },
    { id: 'fade',     name: 'Fade',            desc: 'Blended fade with line-up',   price: 30, mins: 40 },
    { id: 'beard',    name: 'Beard Trim',      desc: 'Shape and hot towel finish',  price: 15, mins: 20 },
    { id: 'combo',    name: 'Haircut + Beard', desc: 'Full cut and beard grooming', price: 38, mins: 50 },
  ];
  const BARBERS = [
    { id: 'any',   name: 'Any available barber', desc: 'Fastest slot' },
    { id: 'b1',    name: 'Aiman',              desc: 'Fades and designs' },
    { id: 'b2',    name: 'Mael',              desc: 'Classic cuts and beards' },
  ];
  const OPEN_HOUR = 10, CLOSE_HOUR = 23, SLOT_STEP = 30; // minutes
  const DAYS_AHEAD = 14;
  const STORAGE_KEY = 'bpb_bookings_v1';

  // ---------- State ----------
  const state = { service: null, barber: null, date: null, time: null };

  // ---------- Storage ----------
  function loadBookings() {
    try { return JSON.parse(localStorage.getItem(STORAGE_KEY)) || []; }
    catch (e) { return []; }
  }
  function saveBookings(list) {
    try { localStorage.setItem(STORAGE_KEY, JSON.stringify(list)); }
    catch (e) { /* storage unavailable; booking still shown for this session */ }
  }

  // ---------- Helpers ----------
  const $ = (sel) => document.querySelector(sel);
  const fmtDateKey = (d) => d.toISOString().slice(0, 10);
  const pad = (n) => String(n).padStart(2, '0');
  const fmtTime = (mins) => pad(Math.floor(mins / 60)) + ':' + pad(mins % 60);
  const fmtLabel = (dateKey) => {
    const [y, m, d] = dateKey.split('-').map(Number);
    return new Date(y, m - 1, d).toLocaleDateString('en-GB', { weekday: 'short', day: 'numeric', month: 'short' });
  };

  function setStep(n) {
    document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
    const target = n === 'done' ? $('#panel-done') : $('#panel-' + n);
    target.classList.add('active');
    document.querySelectorAll('.step-pill').forEach(pill => {
      const s = Number(pill.dataset.step);
      pill.classList.toggle('active', s === n);
      pill.classList.toggle('done', typeof n === 'number' && s < n);
    });
    document.querySelector('#book').scrollIntoView({ behavior: 'smooth' });
  }

  // ---------- Render step 1 ----------
  function renderServices() {
    const wrap = $('#service-options');
    wrap.innerHTML = '';
    SERVICES.forEach(s => {
      const el = document.createElement('div');
      el.className = 'option' + (state.service === s.id ? ' selected' : '');
      el.innerHTML = `<strong>${s.name}</strong><small>${s.desc}</small><small style="display:block">${s.mins} min</small><span class="price">RM ${s.price}</span>`;
      el.addEventListener('click', () => { state.service = s.id; renderServices(); });
      wrap.appendChild(el);
    });
  }

  // ---------- Render step 2 ----------
  function renderBarbers() {
    const wrap = $('#barber-options');
    wrap.innerHTML = '';
    BARBERS.forEach(b => {
      const el = document.createElement('div');
      el.className = 'option' + (state.barber === b.id ? ' selected' : '');
      el.innerHTML = `<strong>${b.name}</strong><small>${b.desc}</small>`;
      el.addEventListener('click', () => {
        state.barber = b.id;
        state.time = null;
        renderBarbers();
        renderDates();
        renderSlots();
      });
      wrap.appendChild(el);
    });
  }

  // ---------- Render step 3 ----------
  function renderDates() {
    const row = $('#date-row');
    row.innerHTML = '';
    const today = new Date();
    today.setHours(0, 0, 0, 0);
    for (let i = 0; i < DAYS_AHEAD; i++) {
      const d = new Date(today);
      d.setDate(today.getDate() + i);
      const key = fmtDateKey(new Date(d.getTime() - d.getTimezoneOffset() * 60000));
      const btn = document.createElement('button');
      btn.className = 'date-chip' + (state.date === key ? ' selected' : '');
      btn.innerHTML = `<small>${d.toLocaleDateString('en-GB', { weekday: 'short' })}</small><strong>${d.getDate()}</strong><small>${d.toLocaleDateString('en-GB', { month: 'short' })}</small>`;
      btn.addEventListener('click', () => {
        state.date = key;
        state.time = null;
        renderDates();
        renderSlots();
      });
      row.appendChild(btn);
    }
  }

  function getTakenSlots(dateKey, barberId) {
    const list = loadBookings();
    return new Set(
      list.filter(b => b.date === dateKey && (barberId === 'any' ? true : b.barber === barberId))
          .map(b => b.time)
    );
  }

  function isPast(dateKey, minutes) {
    const now = new Date();
    const [y, m, d] = dateKey.split('-').map(Number);
    const slot = new Date(y, m - 1, d, Math.floor(minutes / 60), minutes % 60);
    return slot <= now;
  }

  function renderSlots() {
    const grid = $('#slot-grid');
    grid.innerHTML = '';
    if (!state.date) {
      grid.innerHTML = '<p style="color:var(--muted)">Select a date to see available times.</p>';
      return;
    }
    const taken = getTakenSlots(state.date, state.barber || 'any');
    for (let m = OPEN_HOUR * 60; m < CLOSE_HOUR * 60; m += SLOT_STEP) {
      const label = fmtTime(m);
      const btn = document.createElement('button');
      btn.className = 'slot' + (state.time === label ? ' selected' : '');
      btn.textContent = label;
      const unavailable = taken.has(label) || isPast(state.date, m);
      btn.disabled = unavailable;
      btn.addEventListener('click', () => { state.time = label; renderSlots(); });
      grid.appendChild(btn);
    }
  }

  // ---------- Step validation ----------
  function next(from) {
    const err = $('#form-error');
    if (from === 1 && !state.service) return alert('Please choose a service.');
    if (from === 2 && !state.barber) return alert('Please choose a barber.');
    if (from === 3) {
      if (!state.date) return alert('Please pick a date.');
      if (!state.time) return alert('Please pick a time slot.');
    }
    setStep(from + 1);
    if (from + 1 === 3) { renderDates(); renderSlots(); }
  }

  // ---------- Confirm ----------
  function confirmBooking() {
    const err = $('#form-error');
    const name = $('#name').value.trim();
    const phone = $('#phone').value.trim();
    const notes = $('#notes').value.trim();
    if (!name) { err.textContent = 'Please enter your name.'; return; }
    if (!/^[+0-9][0-9 \-]{6,}$/.test(phone)) { err.textContent = 'Please enter a valid phone number.'; return; }

    // Re-check availability in case someone booked this slot meanwhile.
    const taken = getTakenSlots(state.date, state.barber);
    if (taken.has(state.time)) {
      err.textContent = 'Sorry, that slot was just taken. Please pick another time.';
      setStep(3); renderSlots();
      return;
    }

    const svc = SERVICES.find(s => s.id === state.service);
    const barber = BARBERS.find(b => b.id === state.barber);
    const booking = {
      id: Date.now().toString(36) + Math.random().toString(36).slice(2, 6),
      service: svc.name, price: svc.price, mins: svc.mins,
      barber: state.barber, barberName: barber.name,
      date: state.date, time: state.time,
      name, phone, notes,
      createdAt: new Date().toISOString()
    };
    const list = loadBookings();
    list.push(booking);
    saveBookings(list);

    $('#final-summary').innerHTML = `
      <div><span>Service</span><span>${booking.service} · RM ${booking.price}</span></div>
      <div><span>Barber</span><span>${booking.barberName}</span></div>
      <div><span>Date</span><span>${fmtLabel(booking.date)}</span></div>
      <div><span>Time</span><span>${booking.time}</span></div>
      <div><span>Name</span><span>${escapeHtml(booking.name)}</span></div>
      <div><span>Phone</span><span>${escapeHtml(booking.phone)}</span></div>
    `;
    err.textContent = '';
    setStep('done');
  }

  function escapeHtml(s) {
    return s.replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c]));
  }

  function resetBooking() {
    Object.assign(state, { service: null, barber: null, date: null, time: null });
    ['#name', '#phone', '#notes'].forEach(id => $(id).value = '');
    renderServices(); renderBarbers(); renderDates(); renderSlots();
    setStep(1);
  }

  // ---------- Wire up ----------
  document.querySelectorAll('[data-next]').forEach(btn => {
    btn.addEventListener('click', () => {
      const panel = btn.closest('.panel');
      const n = Number(panel.id.replace('panel-', ''));
      next(n);
    });
  });
  document.querySelectorAll('[data-back]').forEach(btn => {
    btn.addEventListener('click', () => {
      const panel = btn.closest('.panel');
      const n = Number(panel.id.replace('panel-', ''));
      setStep(n - 1);
    });
  });
  $('#confirm-btn').addEventListener('click', confirmBooking);
  $('#new-booking').addEventListener('click', resetBooking);

  renderServices();
  renderBarbers();
  renderDates();
  renderSlots();
})();
</script>
</body>
</html>
