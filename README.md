# ELIMINASI-GAUSS-JORDAN-DAN-LELARAN-GAUSS-SEIDEL
export default function GaussEliminationApp() {
  return (
    <div
      dangerouslySetInnerHTML={{
        __html: `
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Eliminasi Gauss-Jordan & Gauss-Seidel</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            line-height: 1.6;
        }
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 25px 50px rgba(0,0,0,0.15);
            overflow: hidden;
        }
        .header {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 40px;
            text-align: center;
        }
        .header h1 {
            font-size: 3em;
            margin-bottom: 15px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        .header p {
            font-size: 1.2em;
            opacity: 0.95;
        }
        .content {
            padding: 40px;
        }
        .method-section {
            margin-bottom: 50px;
            border: 3px solid #e0e0e0;
            border-radius: 15px;
            padding: 30px;
            background: linear-gradient(145deg, #f9f9f9, #ffffff);
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }
        .method-title {
            font-size: 2.2em;
            color: #333;
            margin-bottom: 25px;
            text-align: center;
            padding-bottom: 15px;
            border-bottom: 4px solid #4facfe;
            background: linear-gradient(135deg, #4facfe, #00f2fe);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .examples-section {
            margin-bottom: 30px;
            padding: 25px;
            background: linear-gradient(145deg, #fff8e1, #fff3c4);
            border-radius: 15px;
            border: 3px solid #ffc107;
            box-shadow: 0 10px 25px rgba(255, 193, 7, 0.2);
        }
        .examples-title {
            font-size: 1.5em;
            color: #e65100;
            margin-bottom: 20px;
            text-align: center;
            font-weight: bold;
        }
        .example-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin: 15px 0;
            border: 2px solid #ff9800;
            box-shadow: 0 5px 15px rgba(255, 152, 0, 0.1);
            transition: all 0.3s ease;
        }
        .example-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(255, 152, 0, 0.2);
        }
        .example-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        .example-title {
            font-size: 1.2em;
            font-weight: bold;
            color: #d84315;
        }
        .difficulty-badge {
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.8em;
            font-weight: bold;
            color: white;
        }
        .difficulty-easy { background: #4caf50; }
        .example-problem {
            font-family: monospace;
            font-size: 1.1em;
            margin: 15px 0;
            padding: 15px;
            background: #f5f5f5;
            border-radius: 8px;
            border-left: 4px solid #ff9800;
        }
        .example-buttons {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        .btn-example-use {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        .btn-example-use:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 107, 107, 0.3);
        }
        .input-section {
            margin-bottom: 30px;
            padding: 25px;
            background: #f0f8ff;
            border-radius: 12px;
            border-left: 6px solid #4facfe;
        }
        .input-section h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 1.4em;
        }
        .input-description {
            color: #555;
            margin-bottom: 20px;
            font-style: italic;
        }
        .matrix-input {
            display: grid;
            grid-template-columns: repeat(4, 80px);
            gap: 8px;
            margin-bottom: 25px;
            max-width: 350px;
            justify-content: center;
        }
        .matrix-input input {
            padding: 10px 8px;
            border: 2px solid #ddd;
            border-radius: 8px;
            text-align: center;
            font-size: 14px;
            font-weight: bold;
            transition: all 0.3s ease;
            background: white;
            width: 80px;
        }
        .matrix-input input:focus {
            outline: none;
            border-color: #4facfe;
            box-shadow: 0 0 15px rgba(79, 172, 254, 0.4);
            transform: scale(1.05);
        }
        .matrix-input input:hover {
            border-color: #00f2fe;
        }
        .coefficient-label {
            grid-column: 1 / -1;
            font-weight: bold;
            color: #2c3e50;
            margin-top: 15px;
            margin-bottom: 5px;
        }
        .btn {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            border: none;
            padding: 18px 35px;
            border-radius: 12px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 10px 8px;
            box-shadow: 0 5px 15px rgba(79, 172, 254, 0.3);
        }
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 30px rgba(79, 172, 254, 0.4);
        }
        .btn:active {
            transform: translateY(-1px);
        }
        .results {
            margin-top: 30px;
            padding: 25px;
            background: white;
            border-radius: 15px;
            border: 2px solid #e0e0e0;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }
        .step {
            margin-bottom: 25px;
            padding: 20px;
            background: linear-gradient(145deg, #f0f8ff, #e6f3ff);
            border-radius: 12px;
            border-left: 5px solid #4facfe;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }
        .step h4 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 1.2em;
        }
        .matrix-display {
            font-family: 'Courier New', monospace;
            background: white;
            padding: 20px;
            border-radius: 10px;
            border: 2px solid #e0e0e0;
            margin: 15px 0;
            overflow-x: auto;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.05);
        }
        .matrix-row {
            display: flex;
            justify-content: center;
            margin: 8px 0;
        }
        .matrix-element {
            padding: 12px 15px;
            margin: 3px;
            background: linear-gradient(145deg, #f8f9fa, #e9ecef);
            border: 1px solid #dee2e6;
            border-radius: 8px;
            min-width: 80px;
            text-align: center;
            font-weight: bold;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .matrix-element.pivot {
            background: linear-gradient(145deg, #ffeb3b, #ffc107);
            border-color: #ff9800;
            color: #d84315;
        }
        .solution {
            background: linear-gradient(145deg, #e8f5e8, #c8e6c9);
            border: 3px solid #4caf50;
            padding: 25px;
            border-radius: 15px;
            margin-top: 25px;
            box-shadow: 0 10px 25px rgba(76, 175, 80, 0.2);
        }
        .solution h3 {
            color: #2e7d32;
            margin-bottom: 20px;
            font-size: 1.5em;
            text-align: center;
        }
        .variable-result {
            font-size: 1.3em;
            margin: 15px 0;
            padding: 15px;
            background: white;
            border-radius: 10px;
            border: 2px solid #4caf50;
            text-align: center;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.1);
        }
        .error {
            background: linear-gradient(145deg, #ffebee, #ffcdd2);
            border: 3px solid #f44336;
            padding: 20px;
            border-radius: 12px;
            color: #c62828;
            margin: 15px 0;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(244, 67, 54, 0.2);
        }
        .iteration-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        .iteration-table th,
        .iteration-table td {
            border: 1px solid #ddd;
            padding: 15px;
            text-align: center;
            font-weight: bold;
        }
        .iteration-table th {
            background: linear-gradient(135deg, #4facfe, #00f2fe);
            color: white;
            font-size: 1.1em;
        }
        .iteration-table tr:nth-child(even) {
            background: #f8f9fa;
        }
        .iteration-table tr:hover {
            background: #e3f2fd;
            transform: scale(1.01);
            transition: all 0.2s ease;
        }
        .convergence-info {
            background: linear-gradient(145deg, #e1f5fe, #b3e5fc);
            border: 2px solid #03a9f4;
            border-radius: 10px;
            padding: 15px;
            margin: 15px 0;
            color: #01579b;
            font-weight: bold;
        }
        @media (max-width: 768px) {
            .container {
                margin: 10px;
            }
            .content {
                padding: 20px;
            }
            .matrix-input {
                grid-template-columns: repeat(2, 80px);
                gap: 6px;
            }
            .matrix-input input {
                width: 80px;
                padding: 8px 6px;
                font-size: 13px;
            }
            .header h1 {
                font-size: 2.2em;
            }
            .method-title {
                font-size: 1.8em;
            }
            .example-buttons {
                flex-direction: column;
            }
        }
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid #f3f3f3;
            border-top: 3px solid #4facfe;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🧮 Aplikasi Eliminasi Gauss-Jordan & Gauss-Seidel</h1>
            <p>Solusi Sistem Persamaan Linear dengan Langkah-langkah Detail</p>
        </div>
        <div class="content">
            <!-- Metode Gauss-Jordan -->
            <div class="method-section">
                <h2 class="method-title">📊 Metode Eliminasi Gauss-Jordan</h2>
                                
                <!-- Contoh Soal Gauss-Jordan -->
                <div class="examples-section">
                    <h3 class="examples-title">📚 Contoh Soal Eliminasi Gauss-Jordan</h3>
                                        
                    <div class="example-card">
                        <div class="example-header">
                            <div class="example-title">Contoh: Sistem Linear Sederhana</div>
                            <div class="difficulty-badge difficulty-easy">1</div>
                        </div>
                        <div class="example-problem">
                            <strong>Sistem Persamaan:</strong><br>
                            2x₁ + x₂ - x₃ = 8<br>
                            -3x₁ - x₂ + 2x₃ = -11<br>
                            -2x₁ + x₂ + 2x₃ = -3
                        </div>
                        <div class="example-buttons">
                            <button class="btn-example-use" onclick="useGJExample()">🔄 Gunakan Contoh Ini</button>
                        </div>
                    </div>
                </div>
                                
                <div class="input-section">
                    <h3>🔢 Input Sistem Persamaan Linear (SPL) 3×3</h3>
                    <div class="input-description">
                        Masukkan koefisien dan konstanta untuk sistem persamaan linear 3 variabel
                    </div>
                                        
                    <div class="coefficient-label">Baris 1: a₁₁x₁ + a₁₂x₂ + a₁₃x₃ = b₁</div>
                    <div class="matrix-input">
                        <input type="number" step="any" placeholder="a₁₁" id="gj_0_0" title="Koefisien a₁₁">
                        <input type="number" step="any" placeholder="a₁₂" id="gj_0_1" title="Koefisien a₁₂">
                        <input type="number" step="any" placeholder="a₁₃" id="gj_0_2" title="Koefisien a₁₃">
                        <input type="number" step="any" placeholder="b₁" id="gj_0_3" title="Konstanta b₁">
                    </div>
                                        
                    <div class="coefficient-label">Baris 2: a₂₁x₁ + a₂₂x₂ + a₂₃x₃ = b₂</div>
                    <div class="matrix-input">
                        <input type="number" step="any" placeholder="a₂₁" id="gj_1_0" title="Koefisien a₂₁">
                        <input type="number" step="any" placeholder="a₂₂" id="gj_1_1" title="Koefisien a₂₂">
                        <input type="number" step="any" placeholder="a₂₃" id="gj_1_2" title="Koefisien a₂₃">
                        <input type="number" step="any" placeholder="b₂" id="gj_1_3" title="Konstanta b₂">
                    </div>
                                        
                    <div class="coefficient-label">Baris 3: a₃₁x₁ + a₃₂x₂ + a₃₃x₃ = b₃</div>
                    <div class="matrix-input">
                        <input type="number" step="any" placeholder="a₃₁" id="gj_2_0" title="Koefisien a₃₁">
                        <input type="number" step="any" placeholder="a₃₂" id="gj_2_1" title="Koefisien a₃₂">
                        <input type="number" step="any" placeholder="a₃₃" id="gj_2_2" title="Koefisien a₃₃">
                        <input type="number" step="any" placeholder="b₃" id="gj_2_3" title="Konstanta b₃">
                    </div>
                                        
                    <button class="btn" onclick="solveGaussJordan()">🚀 Selesaikan dengan Gauss-Jordan</button>
                    <button class="btn" onclick="clearGJ()">🗑️ Bersihkan</button>
                </div>
                <div id="gaussJordanResults" class="results" style="display: none;"></div>
            </div>

            <!-- Metode Gauss-Seidel -->
            <div class="method-section">
                <h2 class="method-title">🔄 Metode Gauss-Seidel</h2>
                                
                <!-- Contoh Soal Gauss-Seidel -->
                <div class="examples-section">
                    <h3 class="examples-title">📚 Contoh Soal Gauss-Seidel</h3>
                                        
                    <div class="example-card">
                        <div class="example-header">
                            <div class="example-title">Contoh: Sistem Diagonal Dominan</div>
                            <div class="difficulty-badge difficulty-easy">1</div>
                        </div>
                        <div class="example-problem">
                            <strong>Sistem Persamaan:</strong><br>
                            10x₁ - x₂ + 2x₃ = 6<br>
                            -x₁ + 11x₂ - x₃ = 25<br>
                            2x₁ - x₂ + 10x₃ = -11
                        </div>
                        <div class="example-buttons">
                            <button class="btn-example-use" onclick="useGSExample()">🔄 Gunakan Contoh Ini</button>
                        </div>
                    </div>
                </div>
                                
                <div class="input-section">
                    <h3>🔢 Input Sistem Persamaan Linear (SPL) 3×3</h3>
                    <div class="input-description">
                        Masukkan koefisien dan konstanta untuk metode iteratif Gauss-Seidel
                    </div>
                                        
                    <div class="coefficient-label">Baris 1: a₁₁x₁ + a₁₂x₂ + a₁₃x₃ = b₁</div>
                    <div class="matrix-input">
                        <input type="number" step="any" placeholder="a₁₁" id="gs_0_0" title="Koefisien a₁₁">
                        <input type="number" step="any" placeholder="a₁₂" id="gs_0_1" title="Koefisien a₁₂">
                        <input type="number" step="any" placeholder="a₁₃" id="gs_0_2" title="Koefisien a₁₃">
                        <input type="number" step="any" placeholder="b₁" id="gs_0_3" title="Konstanta b₁">
                    </div>
                                        
                    <div class="coefficient-label">Baris 2: a₂₁x₁ + a₂₂x₂ + a₂₃x₃ = b₂</div>
                    <div class="matrix-input">
                        <input type="number" step="any" placeholder="a₂₁" id="gs_1_0" title="Koefisien a₂₁">
                        <input type="number" step="any" placeholder="a₂₂" id="gs_1_1" title="Koefisien a₂₂">
                        <input type="number" step="any" placeholder="a₂₃" id="gs_1_2" title="Koefisien a₂₃">
                        <input type="number" step="any" placeholder="b₂" id="gs_1_3" title="Konstanta b₂">
                    </div>
                                        
                    <div class="coefficient-label">Baris 3: a₃₁x₁ + a₃₂x₂ + a₂₃x₃ = b₃</div>
                    <div class="matrix-input">
                        <input type="number" step="any" placeholder="a₃₁" id="gs_2_0" title="Koefisien a₃₁">
                        <input type="number" step="any" placeholder="a₃₂" id="gs_2_1" title="Koefisien a₃₂">
                        <input type="number" step="any" placeholder="a₃₃" id="gs_2_2" title="Koefisien a₂₃">
                        <input type="number" step="any" placeholder="b₃" id="gs_2_3" title="Konstanta b₃">
                    </div>
                                        
                    <div style="margin: 25px 0; padding: 20px; background: #f0f8ff; border-radius: 10px;">
                        <label style="font-weight: bold; color: #2c3e50;">⚙️ Toleransi Error: </label>
                        <input type="number" step="any" value="0.0001" id="tolerance" style="padding: 10px; border: 2px solid #ddd; border-radius: 8px; margin: 0 10px;">
                                                
                        <label style="margin-left: 25px; font-weight: bold; color: #2c3e50;">🔄 Maksimum Iterasi: </label>
                        <input type="number" value="100" id="maxIterations" style="padding: 10px; border: 2px solid #ddd; border-radius: 8px; margin: 0 10px;">
                    </div>
                                        
                    <button class="btn" onclick="solveGaussSeidel()">🚀 Selesaikan dengan Gauss-Seidel</button>
                    <button class="btn" onclick="clearGS()">🗑️ Bersihkan</button>
                </div>
                <div id="gaussSeidelResults" class="results" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        // Fungsi untuk menggunakan contoh Gauss-Jordan
        function useGJExample() {
            const example = [
                [2, 1, -1, 8],
                [-3, -1, 2, -11],
                [-2, 1, 2, -3]
            ];
            for (let i = 0; i < 3; i++) {
                for (let j = 0; j < 4; j++) {
                    document.getElementById(\`gj_\${i}_\${j}\`).value = example[i][j];
                }
            }
            document.querySelector('.input-section').scrollIntoView({ behavior: 'smooth' });
        }

        // Fungsi untuk menggunakan contoh Gauss-Seidel
        function useGSExample() {
            const example = [
                [10, -1, 2, 6],
                [-1, 11, -1, 25],
                [2, -1, 10, -11]
            ];
            for (let i = 0; i < 3; i++) {
                for (let j = 0; j < 4; j++) {
                    document.getElementById(\`gs_\${i}_\${j}\`).value = example[i][j];
                }
            }
            const gsInputSection = document.querySelectorAll('.input-section')[1];
            gsInputSection.scrollIntoView({ behavior: 'smooth' });
        }

        // Fungsi untuk membersihkan input Gauss-Jordan
        function clearGJ() {
            for (let i = 0; i < 3; i++) {
                for (let j = 0; j < 4; j++) {
                    document.getElementById(\`gj_\${i}_\${j}\`).value = '';
                }
            }
            document.getElementById('gaussJordanResults').style.display = 'none';
        }

        // Fungsi untuk membersihkan input Gauss-Seidel
        function clearGS() {
            for (let i = 0; i < 3; i++) {
                for (let j = 0; j < 4; j++) {
                    document.getElementById(\`gs_\${i}_\${j}\`).value = '';
                }
            }
            document.getElementById('gaussSeidelResults').style.display = 'none';
        }

        // Fungsi untuk menampilkan matriks dengan highlighting pivot
        function displayMatrix(matrix, title = "", pivotRow = -1, pivotCol = -1) {
            let html = \`<div class="matrix-display">\`;
            if (title) html += \`<h4>\${title}</h4>\`;
                        
            for (let i = 0; i < matrix.length; i++) {
                html += \`<div class="matrix-row">\`;
                for (let j = 0; j < matrix[i].length; j++) {
                    const value = typeof matrix[i][j] === 'number' ?
                         (Math.abs(matrix[i][j]) < 1e-10 ? '0' : matrix[i][j].toFixed(6)) :
                         matrix[i][j];
                    const isPivot = (i === pivotRow && j === pivotCol);
                    const className = isPivot ? 'matrix-element pivot' : 'matrix-element';
                    html += \`<div class="\${className}">\${value}</div>\`;
                }
                html += \`</div>\`;
            }
            html += \`</div>\`;
            return html;
        }

        // Fungsi untuk menyelesaikan dengan Gauss-Jordan
        function solveGaussJordan() {
            try {
                // Ambil input matriks
                const matrix = [];
                for (let i = 0; i < 3; i++) {
                    matrix[i] = [];
                    for (let j = 0; j < 4; j++) {
                        const value = parseFloat(document.getElementById(\`gj_\${i}_\${j}\`).value);
                        if (isNaN(value)) {
                            throw new Error(\`Nilai pada baris \${i+1}, kolom \${j+1} tidak valid atau kosong\`);
                        }
                        matrix[i][j] = value;
                    }
                }

                let html = \`<h3>🔍 Langkah-langkah Eliminasi Gauss-Jordan</h3>\`;
                                
                // Tampilkan sistem persamaan awal
                html += \`<div class="step">\`;
                html += \`<h4>📋 Sistem Persamaan Linear Awal:</h4>\`;
                for (let i = 0; i < 3; i++) {
                    let equation = '';
                    for (let j = 0; j < 3; j++) {
                        if (j === 0) {
                            equation += \`\${matrix[i][j]}x\${j+1}\`;
                        } else {
                            equation += matrix[i][j] >= 0 ? \` + \${matrix[i][j]}x\${j+1}\` : \` - \${Math.abs(matrix[i][j])}x\${j+1}\`;
                        }
                    }
                    equation += \` = \${matrix[i][3]}\`;
                    html += \`<div style="margin: 8px 0; font-family: monospace; font-size: 1.1em; font-weight: bold;">\${equation}</div>\`;
                }
                html += \`</div>\`;

                html += displayMatrix(matrix, "🔢 Matriks Augmented Awal:");

                // Proses eliminasi Gauss-Jordan
                const steps = [];
                let stepCount = 1;

                // Forward elimination dan back substitution
                for (let i = 0; i < 3; i++) {
                    // Cari pivot terbesar (partial pivoting)
                    let maxRow = i;
                    for (let k = i + 1; k < 3; k++) {
                        if (Math.abs(matrix[k][i]) > Math.abs(matrix[maxRow][i])) {
                            maxRow = k;
                        }
                    }

                    // Tukar baris jika perlu
                    if (maxRow !== i) {
                        [matrix[i], matrix[maxRow]] = [matrix[maxRow], matrix[i]];
                        steps.push({
                            step: stepCount++,
                            description: \`🔄 Tukar baris \${i+1} dengan baris \${maxRow+1} (Partial Pivoting)\`,
                            matrix: matrix.map(row => [...row]),
                            pivotRow: i,
                            pivotCol: i
                        });
                    }

                    // Cek apakah pivot adalah nol
                    if (Math.abs(matrix[i][i]) < 1e-10) {
                        throw new Error(\`❌ Sistem tidak memiliki solusi unik (pivot nol pada baris \${i+1})\`);
                    }

                    // Normalisasi baris pivot (buat diagonal = 1)
                    const pivot = matrix[i][i];
                    if (Math.abs(pivot - 1) > 1e-10) {
                        for (let j = 0; j < 4; j++) {
                            matrix[i][j] /= pivot;
                        }
                        steps.push({
                            step: stepCount++,
                            description: \`➗ R\${i+1} = R\${i+1} ÷ \${pivot.toFixed(6)} (Normalisasi pivot)\`,
                            matrix: matrix.map(row => [...row]),
                            pivotRow: i,
                            pivotCol: i
                        });
                    }

                    // Eliminasi kolom (buat elemen lain = 0)
                    for (let k = 0; k < 3; k++) {
                        if (k !== i && Math.abs(matrix[k][i]) > 1e-10) {
                            const factor = matrix[k][i];
                            for (let j = 0; j < 4; j++) {
                                matrix[k][j] -= factor * matrix[i][j];
                            }
                            steps.push({
                                step: stepCount++,
                                description: \`🧮 R\${k+1} = R\${k+1} - (\${factor.toFixed(6)}) × R\${i+1}\`,
                                matrix: matrix.map(row => [...row]),
                                pivotRow: i,
                                pivotCol: i
                            });
                        }
                    }
                }

                // Tampilkan langkah-langkah
                steps.forEach(step => {
                    html += \`<div class="step">\`;
                    html += \`<h4>📍 Langkah \${step.step}: \${step.description}</h4>\`;
                    html += displayMatrix(step.matrix, "", step.pivotRow, step.pivotCol);
                    html += \`</div>\`;
                });

                // Tampilkan solusi
                html += \`<div class="solution">\`;
                html += \`<h3>🎉 Solusi Sistem Persamaan Linear</h3>\`;
                html += \`<div class="variable-result">x₁ = \${matrix[0][3].toFixed(8)}</div>\`;
                html += \`<div class="variable-result">x₂ = \${matrix[1][3].toFixed(8)}</div>\`;
                html += \`<div class="variable-result">x₃ = \${matrix[2][3].toFixed(8)}</div>\`;
                html += \`</div>\`;

                document.getElementById('gaussJordanResults').innerHTML = html;
                document.getElementById('gaussJordanResults').style.display = 'block';
            } catch (error) {
                document.getElementById('gaussJordanResults').innerHTML =
                     \`<div class="error">❌ Error: \${error.message}</div>\`;
                document.getElementById('gaussJordanResults').style.display = 'block';
            }
        }

        // Fungsi untuk menyelesaikan dengan Gauss-Seidel
        function solveGaussSeidel() {
            try {
                // Ambil input matriks
                const A = [];
                const b = [];
                for (let i = 0; i < 3; i++) {
                    A[i] = [];
                    for (let j = 0; j < 3; j++) {
                        const value = parseFloat(document.getElementById(\`gs_\${i}_\${j}\`).value);
                        if (isNaN(value)) {
                            throw new Error(\`Nilai koefisien pada baris \${i+1}, kolom \${j+1} tidak valid atau kosong\`);
                        }
                        A[i][j] = value;
                    }
                    const bValue = parseFloat(document.getElementById(\`gs_\${i}_3\`).value);
                    if (isNaN(bValue)) {
                        throw new Error(\`Nilai konstanta pada baris \${i+1} tidak valid atau kosong\`);
                    }
                    b[i] = bValue;
                }

                const tolerance = parseFloat(document.getElementById('tolerance').value) || 0.0001;
                const maxIter = parseInt(document.getElementById('maxIterations').value) || 100;

                let html = \`<h3>🔄 Metode Gauss-Seidel - Langkah-langkah Iterasi</h3>\`;
                                
                // Tampilkan sistem persamaan
                html += \`<div class="step">\`;
                html += \`<h4>📋 Sistem Persamaan Linear:</h4>\`;
                for (let i = 0; i < 3; i++) {
                    let equation = '';
                    for (let j = 0; j < 3; j++) {
                        if (j === 0) {
                            equation += \`\${A[i][j]}x\${j+1}\`;
                        } else {
                            equation += A[i][j] >= 0 ? \` + \${A[i][j]}x\${j+1}\` : \` - \${Math.abs(A[i][j])}x\${j+1}\`;
                        }
                    }
                    equation += \` = \${b[i]}\`;
                    html += \`<div style="margin: 8px 0; font-family: monospace; font-size: 1.1em; font-weight: bold;">\${equation}</div>\`;
                }
                html += \`</div>\`;

                // Iterasi Gauss-Seidel
                let x = [0, 0, 0]; // Tebakan awal
                let iterations = [];
                let converged = false;

                // Tambahkan iterasi awal
                iterations.push({
                    iter: 0,
                    x1: x[0],
                    x2: x[1],
                    x3: x[2],
                    error: '-'
                });

                for (let iter = 1; iter <= maxIter; iter++) {
                    let xOld = [...x];
                                        
                    // Update setiap variabel menggunakan nilai terbaru
                    for (let i = 0; i < 3; i++) {
                        let sum = b[i];
                        for (let j = 0; j < 3; j++) {
                            if (i !== j) {
                                sum -= A[i][j] * x[j];
                            }
                        }
                        x[i] = sum / A[i][i];
                    }

                    // Hitung error maksimum
                    let maxError = 0;
                    for (let i = 0; i < 3; i++) {
                        const error = Math.abs(x[i] - xOld[i]);
                        if (error > maxError) maxError = error;
                    }

                    iterations.push({
                        iter: iter,
                        x1: x[0],
                        x2: x[1],
                        x3: x[2],
                        error: maxError
                    });

                    if (maxError < tolerance) {
                        converged = true;
                        break;
                    }
                }

                // Tampilkan tabel iterasi
                html += \`<div class="step">\`;
                html += \`<h4>📊 Tabel Iterasi:</h4>\`;
                html += \`<table class="iteration-table">\`;
                html += \`<tr><th>Iterasi</th><th>x₁</th><th>x₂</th><th>x₃</th><th>Error Maksimum</th><th>Status</th></tr>\`;
                                
                iterations.forEach((iter, index) => {
                    const status = index === 0 ? 'Awal' :
                                  (typeof iter.error === 'number' && iter.error < tolerance) ? '✅ Konvergen' :
                                  index === iterations.length - 1 && !converged ? '⏹️ Max Iter' : '🔄 Iterasi';
                    html += \`<tr>\`;
                    html += \`<td>\${iter.iter}</td>\`;
                    html += \`<td>\${typeof iter.x1 === 'number' ? iter.x1.toFixed(8) : iter.x1}</td>\`;
                    html += \`<td>\${typeof iter.x2 === 'number' ? iter.x2.toFixed(8) : iter.x2}</td>\`;
                    html += \`<td>\${typeof iter.x3 === 'number' ? iter.x3.toFixed(8) : iter.x3}</td>\`;
                    html += \`<td>\${typeof iter.error === 'number' ? iter.error.toFixed(10) : iter.error}</td>\`;
                    html += \`<td>\${status}</td>\`;
                    html += \`</tr>\`;
                });
                                
                html += \`</table>\`;
                html += \`</div>\`;

                // Tampilkan solusi
                if (converged) {
                    html += \`<div class="solution">\`;
                    html += \`<h3>🎉 Solusi Konvergen!</h3>\`;
                    html += \`<div style="text-align: center; margin-bottom: 20px;">\`;
                    html += \`<strong>Iterasi ke-\${iterations.length - 1} | Toleransi: \${tolerance} | Error: \${iterations[iterations.length - 1].error.toFixed(10)}</strong>\`;
                    html += \`</div>\`;
                    html += \`<div class="variable-result">x₁ = \${x[0].toFixed(10)}</div>\`;
                    html += \`<div class="variable-result">x₂ = \${x[1].toFixed(10)}</div>\`;
                    html += \`<div class="variable-result">x₃ = \${x[2].toFixed(10)}</div>\`;
                    html += \`</div>\`;
                } else {
                    html += \`<div class="error">\`;
                    html += \`❌ Solusi tidak konvergen setelah \${maxIter} iterasi.<br>\`;
                    html += \`Error terakhir: \${iterations[iterations.length - 1].error.toFixed(10)}<br>\`;
                    html += \`Saran: Tingkatkan jumlah iterasi maksimum atau periksa kondisi diagonal dominance.\`;
                    html += \`</div>\`;
                }

                document.getElementById('gaussSeidelResults').innerHTML = html;
                document.getElementById('gaussSeidelResults').style.display = 'block';
            } catch (error) {
                document.getElementById('gaussSeidelResults').innerHTML =
                     \`<div class="error">❌ Error: \${error.message}</div>\`;
                document.getElementById('gaussSeidelResults').style.display = 'block';
            }
        }

        // Event listeners untuk input validation
        document.addEventListener('DOMContentLoaded', function() {
            // Validasi input hanya angka
            const inputs = document.querySelectorAll('input[type="number"]');
            inputs.forEach(input => {
                input.addEventListener('input', function() {
                    if (this.value && isNaN(parseFloat(this.value))) {
                        this.style.borderColor = '#f44336';
                        this.style.backgroundColor = '#ffebee';
                    } else {
                        this.style.borderColor = '#ddd';
                        this.style.backgroundColor = 'white';
                    }
                });
            });

            // Auto-scroll ke hasil setelah perhitungan
            const observer = new MutationObserver(function(mutations) {
                mutations.forEach(function(mutation) {
                    if (mutation.type === 'attributes' && mutation.attributeName === 'style') {
                        const target = mutation.target;
                        if (target.id === 'gaussJordanResults' || target.id === 'gaussSeidelResults') {
                            if (target.style.display === 'block') {
                                setTimeout(() => {
                                    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                                }, 100);
                            }
                        }
                    }
                });
            });

            // Observe hasil sections
            const gjResults = document.getElementById('gaussJordanResults');
            const gsResults = document.getElementById('gaussSeidelResults');
            if (gjResults) observer.observe(gjResults, { attributes: true });
            if (gsResults) observer.observe(gsResults, { attributes: true });
        });
    </script>
</body>
</html>
      `,
      }}
    />
  )
}
