<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>Undang-Undang Kepolisian Mandalika</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body { font-family: Arial, sans-serif; background:#f4f6f8; margin:0; padding:20px; }
    h1 { text-align:center; }
    table { width:100%; border-collapse:collapse; margin-top:15px; background:#fff; }
    th, td { border:1px solid #ccc; padding:8px; text-align:left; }
    th { background:#2c3e50; color:#fff; }
    tr:nth-child(even){ background:#f2f2f2; }
    .container { max-width:1200px; margin:auto; }
    .rekap { margin-top:30px; }
    button { padding:6px 10px; cursor:pointer; }
    .copy-btn { background:#3498db; color:#fff; border:none; border-radius:4px; }
    .copy-btn:hover { background:#2980b9; }
  </style>
</head>
<body>
<div class="container">
  <h1>Database Undang-Undang Kepolisian RP</h1>

  <!-- TABLE UU -->
  <h2>Pasal Ringan</h2>
  <table id="uuTable">
    <thead>
      <tr>
        <th>Pilih</th>
        <th>Pasal</th>
        <th>Deskripsi</th>
        <th>Denda</th>
        <th>Masa Tahanan</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.1</td>
        <td>Tidak Memiliki SIM Kendaraan</td>
        <td>$10</td>
        <td>5 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.2</td>
        <td>Melawan Arah Saat Berkendara</td>
        <td>$10</td>
        <td>5 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.3</td>
        <td>Upaya Menyogok Petugas</td>
        <td>$15</td>
        <td>10 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.4</td>
        <td>Membawa Hewan Dilindungi (Penyu, Hiu, Lumba-lumba)</td>
        <td>$15</td>
        <td>10 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.5</td>
        <td>Membuat Kerusuhan di Keramaian</td>
        <td>$20</td>
        <td>10 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.6</td>
        <td>Memberikan Informasi Palsu</td>
        <td>$20</td>
        <td>10 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.7</td>
        <td>Sengaja / Tidak Sengaja Berada di TKP Penembakan</td>
        <td>$30</td>
        <td>15 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.8</td>
        <td>Tidak Melengkapi Atribut Saat Berkendara</td>
        <td>$8</td>
        <td>5 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 0.9</td>
        <td>Menggunakan Atribut Kepolisian</td>
        <td>$13</td>
        <td>20 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 1.0</td>
        <td>Menghina Faction (Kepolisian, EMS, Pemerintah, Pedagang)</td>
        <td>$50</td>
        <td>30 Bulan</td>
      </tr>
      <tr>
        <td><input type="checkbox" onchange="updateRekap(this)"></td>
        <td>Pasal 1.1</td>
        <td>Melakukan Perjudian</td>
        <td>$20</td>
        <td>25 Bulan</td>
      </tr>
    </tbody>
  </table>

  <h2>Pasal Sedang</h2>
  <p><i>(Belum tersedia)</i></p>

  <h2>Pasal Berat</h2>
  <p><i>(Belum tersedia)</i></p>

  <!-- REKAP -->
  <div class="rekap">
    <h2>Rekapan Pasal Terpilih</h2>
    <table id="rekapTable">
      <thead>
        <tr>
          <th>Pasal</th>
          <th>Denda</th>
          <th>Masa Tahanan</th>
          <th>Aksi</th>
        </tr>
      </thead>
      <tbody></tbody>
      <tfoot>
        <tr>
          <th>Total</th>
          <th id="totalDenda">$0</th>
          <th id="totalTahanan">0 Bulan</th>
          <th>
            <button class="copy-btn" onclick="copyAll()">Copy Semua</button>
          </th>
        </tr>
      </tfoot>
    </table>
  </div>
</div>

<script>
function updateRekap(checkbox) {
  const row = checkbox.parentElement.parentElement;
  const pasal = row.cells[1].innerText;
  const denda = row.cells[3].innerText;
  const tahanan = row.cells[4].innerText;
  const tbody = document.querySelector('#rekapTable tbody');

  if (checkbox.checked) {
    const tr = document.createElement('tr');
    tr.setAttribute('data-pasal', pasal);
    tr.setAttribute('data-denda', parseInt(denda.replace('$','')));
    tr.setAttribute('data-tahanan', parseInt(tahanan));
    tr.innerHTML = `
      <td>${pasal}</td>
      <td>${denda}</td>
      <td>${tahanan}</td>
      <td><button class="copy-btn" onclick="copyPasal('${pasal}','${denda}','${tahanan}')">Copy</button></td>
    `;
    tbody.appendChild(tr);
  } else {
    const rows = tbody.querySelectorAll('tr');
    rows.forEach(r => {
      if (r.getAttribute('data-pasal') === pasal) r.remove();
    });
  }
  hitungTotal();
}</td>
      <td>${denda}</td>
      <td>${tahanan}</td>
      <td><button class="copy-btn" onclick="copyPasal('${pasal}','${denda}','${tahanan}')">Copy</button></td>
    `;
    tbody.appendChild(tr);
  } else {
    const rows = tbody.querySelectorAll('tr');
    rows.forEach(r => {
      if (r.getAttribute('data-pasal') === pasal) r.remove();
    });
  }
}

function copyPasal(pasal, denda, tahanan) {
  const text = `${pasal} | Denda: ${denda} | Masa Tahanan: ${tahanan}`;
  navigator.clipboard.writeText(text);
}

function hitungTotal() {
  let totalDenda = 0;
  let totalTahanan = 0;
  document.querySelectorAll('#rekapTable tbody tr').forEach(row => {
    totalDenda += parseInt(row.getAttribute('data-denda'));
    totalTahanan += parseInt(row.getAttribute('data-tahanan'));
  });
  document.getElementById('totalDenda').innerText = '$' + totalDenda;
  document.getElementById('totalTahanan').innerText = totalTahanan + ' Bulan';
}

function copyAll() {
  let text = 'Pasal yang Dilanggar:
';
  document.querySelectorAll('#rekapTable tbody tr').forEach(row => {
    text += row.cells[0].innerText + ' | ' + row.cells[1].innerText + ' | ' + row.cells[2].innerText + '
';
  });
  text += `Total Denda: ${document.getElementById('totalDenda').innerText}
`;
  text += `Total Penjara: ${document.getElementById('totalTahanan').innerText}`;
  navigator.clipboard.writeText(text);
} | Denda: ${denda} | Masa Tahanan: ${tahanan}`;
  navigator.clipboard.writeText(text);
  alert('Pasal berhasil di copy!');
}
</script>
</body>
</html>
