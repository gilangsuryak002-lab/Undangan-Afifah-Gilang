<!DOCTYPE html><html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Undangan Pernikahan – Web</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
    body{font-family:Inter, sans-serif; background:#f8fafc; margin:0; color:#0f172a}
    .container{width:min(1000px,92%);margin:auto;padding:1rem}
    h1,h2{font-family:"Playfair Display",serif}
    .card{background:#fff;padding:1rem;border:1px solid #e2e8f0;border-radius:14px;box-shadow:0 6px 20px rgba(0,0,0,.06);margin-bottom:1rem}
    .btn{display:inline-block;padding:.6rem 1rem;background:#4f46e5;color:#fff;border-radius:10px;text-decoration:none;margin:.2rem 0}
    .list{list-style:none;padding:0;margin:0}
    .list li{padding:.4rem 0;border-bottom:1px solid #e2e8f0}
  </style>
</head>
<body>
  <div class="container">
    <header class="card">
      <h1 id="names">A & B</h1>
      <p id="dateText">Minggu, 12 Oktober 2025 · Bandung</p>
      <p>Yth. <span id="guestName">Tamu Undangan</span>,</p>
      <p>Dengan hormat, kami mengundang Anda untuk hadir pada acara pernikahan kami.</p>
    </header><section class="card">
  <h2>Konfirmasi Kehadiran</h2>
  <p>Silakan isi nama Anda dan pilih status kehadiran:</p>
  <form id="formRSVP">
    <input type="text" id="guestInput" placeholder="Nama Anda" style="padding:.6rem; width:100%; margin-bottom:.6rem; border:1px solid #ddd; border-radius:8px" required />
    <select id="statusInput" style="padding:.6rem; width:100%; margin-bottom:.6rem; border:1px solid #ddd; border-radius:8px">
      <option value="Hadir">Hadir</option>
      <option value="Tidak Hadir">Tidak Hadir</option>
    </select>
    <button class="btn" type="submit">Kirim</button>
  </form>
</section>

<section class="card">
  <h2>Daftar Tamu yang Konfirmasi</h2>
  <ul id="guestList" class="list"></ul>
</section>

  </div>  <script>
    const params = new URLSearchParams(window.location.search);
    const tamu = params.get('to');
    if(tamu){
      document.getElementById('guestName').textContent = tamu;
    }

    const guestListEl = document.getElementById('guestList');
    let guests = JSON.parse(localStorage.getItem('guests')||'[]');

    function renderGuests(){
      guestListEl.innerHTML = '';
      guests.forEach(g=>{
        const li=document.createElement('li');
        li.textContent = `${g.name} – ${g.status}`;
        guestListEl.appendChild(li);
      });
    }

    document.getElementById('formRSVP').addEventListener('submit', e=>{
      e.preventDefault();
      const name=document.getElementById('guestInput').value.trim();
      const status=document.getElementById('statusInput').value;
      if(!name) return;
      guests.push({name,status});
      localStorage.setItem('guests', JSON.stringify(guests));
      document.getElementById('guestInput').value='';
      renderGuests();
    });

    renderGuests();
  </script></body>
</html>
