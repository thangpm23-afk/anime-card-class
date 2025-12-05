<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Tính EXP & Sách</title>
<style>
  body { font-family: Arial, sans-serif; max-width: 700px; margin: 20px auto; }
  input, button { padding: 5px; margin: 5px; width: 100px; }
  table { border-collapse: collapse; margin-top: 10px; }
  th, td { border: 1px solid #aaa; padding: 5px 10px; }
</style>
</head>
<body>
  <h2>Tính EXP & Sử dụng Sách</h2>

  <label>Cấp bắt đầu:</label>
  <input type="number" id="startLevel" value="0"><br>

  <label>Cấp kết thúc:</label>
  <input type="number" id="endLevel" value="10"><br><br>

  <h3>Nhập số sách bạn có:</h3>
  <label>50 EXP:</label> <input type="number" id="book50" value="0"><br>
  <label>100 EXP:</label> <input type="number" id="book100" value="0"><br>
  <label>250 EXP:</label> <input type="number" id="book250" value="0"><br>
  <label>500 EXP:</label> <input type="number" id="book500" value="0"><br>
  <label>1000 EXP:</label> <input type="number" id="book1000" value="0"><br><br>

  <button onclick="calculateEXP()">Tính EXP & Số sách</button>

  <h3 id="result"></h3>
  <h3 id="usedBooks"></h3>

<script>
function calculateEXP() {
    const start = parseInt(document.getElementById('startLevel').value);
    const end = parseInt(document.getElementById('endLevel').value);

    if (isNaN(start) || isNaN(end) || end <= start) {
        document.getElementById('result').innerText = 
          "Vui lòng nhập cấp hợp lệ (cấp kết thúc > cấp bắt đầu).";
        return;
    }

    // Tính tổng EXP cần
    let totalEXP = 0;
    for (let i = start + 1; i <= end; i++) {
        totalEXP += i * 100;
    }
    document.getElementById('result').innerText = 
      `Tổng EXP từ cấp ${start} lên cấp ${end} là: ${totalEXP.toLocaleString()} EXP`;

    // Sách có sẵn
    let books = [
        {exp: 1000, count: parseInt(document.getElementById('book1000').value)},
        {exp: 500, count: parseInt(document.getElementById('book500').value)},
        {exp: 250, count: parseInt(document.getElementById('book250').value)},
        {exp: 100, count: parseInt(document.getElementById('book100').value)},
        {exp: 50, count: parseInt(document.getElementById('book50').value)},
    ];

    let expLeft = totalEXP;
    let usedBooks = [];

    for (let book of books) {
        let use = Math.min(Math.floor(expLeft / book.exp), book.count);
        expLeft -= use * book.exp;
        usedBooks.push(`${use} cuốn ${book.exp} EXP`);
    }

    let resultText = `Sử dụng sách để đạt mục tiêu:\n` + usedBooks.join(', ');
    if (expLeft > 0) {
        resultText += `\nCòn thiếu: ${expLeft} EXP`;
    }

    document.getElementById('usedBooks').innerText = resultText;
}
</script>

</body>
</html>
