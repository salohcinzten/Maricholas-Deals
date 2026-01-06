# Maricholas-Deals
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maricholas Deals | Live Inventory</title>
    <style>
        :root { --gold: #d4af37; --dark: #1a1a1a; --cream: #fdf6e3; }
        body { font-family: sans-serif; background: var(--cream); margin: 0; text-align: center; }
        .navbar { background: var(--dark); color: var(--gold); padding: 20px; border-bottom: 4px solid var(--gold); }
        .inventory-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 20px; padding: 20px; }
        .card { background: white; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); padding: 15px; }
        .card img { width: 100%; border-radius: 5px; height: 150px; object-fit: cover; }
        .price { color: #b35900; font-weight: bold; font-size: 20px; }
        .btn { display: block; background: var(--dark); color: var(--gold); padding: 10px; text-decoration: none; margin-top: 10px; border-radius: 5px; }
    </style>
</head>
<body>

<div class="navbar">
    <h1>MARICHOLAS DEALS</h1>
    <p>Live Inventory Feed</p>
</div>

<div class="inventory-grid" id="content">Loading latest deals...</div>

<script>
    // PASTE YOUR PUBLISHED GOOGLE SHEETS LINK HERE
    const sheetURL = 'REPLACE_THIS_WITH_YOUR_CSV_LINK';

    async function getSheetData() {
        const response = await fetch(sheetURL);
        const data = await response.text();
        const rows = data.split('\n').slice(1); // Skip the header row
        
        let html = '';
        rows.forEach(row => {
            const columns = row.split(',');
            if (columns.length >= 4) {
                html += `
                    <div class="card">
                        <img src="${columns[4]}" alt="product">
                        <h3>${columns[0]}</h3>
                        <div class="price">${columns[1]}</div>
                        <p>${columns[2]}</p>
                        <small>Status: ${columns[3]}</small>
                        <a href="https://wa.me/YOUR_NUMBER" class="btn">ORDER NOW</a>
                    </div>
                `;
            }
        });
        document.getElementById('content').innerHTML = html;
    }

    getSheetData();
</script>
</body>
</html>
