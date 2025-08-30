[index.html.html](https://github.com/user-attachments/files/22060868/index.html.html)
<!-- Chosen Palette: Warm Neutrals & Subtle Accents -->
<!-- Application Structure Plan: A single-page dashboard layout organized into thematic sections. The flow starts with a high-level overview (Portfolio Composition), then dives into a detailed analysis of the main asset class (Ações Brasileiras), covering performance (ROE), valuation (P/L, P/VP), and risk (Debt). It then visualizes a portfolio-wide characteristic (5-Year Volatility) and finishes with dedicated sections for other asset classes (FIIs, ETFs). This narrative structure guides the user from the general to the specific, making complex data easier to understand than a simple table. -->
<!-- Visualization & Content Choices: 
- Portfolio Composition: Goal: Organize. Viz: Donut Chart. Justification: Ideal for showing the proportional breakdown of asset classes. Library: Chart.js/Canvas.
- Stock ROE: Goal: Compare. Viz: Bar Chart. Justification: Effectively compares the profitability metric across different companies. Library: Chart.js/Canvas.
- Stock Valuation (P/L & P/VP): Goal: Compare. Viz: Grouped Bar Chart. Justification: Allows simultaneous comparison of two key valuation metrics for each stock. Library: Chart.js/Canvas.
- 5-Year Price Range: Goal: Change/Compare. Viz: Floating Horizontal Bar Chart on a logarithmic scale. Justification: Best way to visualize the vast volatility differences between all assets (especially BTC vs. others) while maintaining readability. Library: Chart.js/Canvas.
- FII P/VP: Goal: Compare. Viz: Simple Bar Chart. Justification: Clearly shows if FIIs are trading at a discount or premium to their net asset value. Library: Chart.js/Canvas.
- ETFs Overview: Goal: Inform. Viz: Styled HTML Cards. Justification: Since numerical comparison is not applicable, descriptive cards provide essential context on the strategy of each ETF. Method: HTML/CSS with Tailwind.
-->
<!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard de Análise de Portfólio</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #F8F7F4; /* Warm Neutral */
            color: #4A4A4A;
        }
        .chart-container {
            position: relative;
            width: 100%;
            height: 40vh;
            max-height: 400px;
        }
        .card {
            background-color: #FFFFFF;
            border: 1px solid #EAEAEA;
        }
    </style>
</head>
<body class="p-4 sm:p-6 md:p-8">
    <div class="max-w-7xl mx-auto">
        <header class="text-center mb-12">
            <h1 class="text-4xl md:text-5xl font-bold text-[#3A868C] mb-2">Análise de Portfólio de Investimentos</h1>
            <p class="text-lg text-gray-600">Um dashboard interativo para visualizar a saúde e performance dos seus ativos.</p>
        </header>

        <main class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            
            <section class="md:col-span-1 card rounded-2xl shadow-lg p-6">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">Composição da Carteira</h2>
                <p class="text-gray-600 mb-6">A diversificação entre diferentes classes de ativos é fundamental. Este gráfico mostra a distribuição percentual do seu portfólio, revelando a concentração em cada tipo de investimento.</p>
                <div class="chart-container" style="max-height: 350px;">
                    <canvas id="portfolioCompositionChart"></canvas>
                </div>
            </section>

            <section class="md:col-span-1 card rounded-2xl shadow-lg p-6">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">Análise de FIIs (P/VP)</h2>
                <p class="text-gray-600 mb-6">O indicador Preço/Valor Patrimonial (P/VP) é crucial para Fundos Imobiliários. Valores próximos a 1 indicam preço justo, abaixo de 1 um possível desconto, e acima, um ágio.</p>
                <div class="chart-container" style="max-height: 350px;">
                    <canvas id="fiiChart"></canvas>
                </div>
            </section>
            
            <section class="md:col-span-2 lg:col-span-1 card rounded-2xl shadow-lg p-6 flex flex-col justify-between">
                <div>
                    <h2 class="text-2xl font-bold text-gray-800 mb-4">ETFs: Estratégia e Exposição</h2>
                    <p class="text-gray-600 mb-6">Seus ETFs proporcionam diversificação automática em mercados e estratégias distintas.</p>
                </div>
                <div class="space-y-4">
                    <div class="p-3 rounded-lg bg-gray-50 border">
                        <h3 class="font-bold text-[#3A868C]">BOVA11 & IVV</h3>
                        <p class="text-gray-600 text-sm">Exposição aos principais índices do Brasil (Ibovespa) e dos EUA (S&P 500).</p>
                    </div>
                     <div class="p-3 rounded-lg bg-gray-50 border">
                        <h3 class="font-bold text-[#3A868C]">SCHD</h3>
                        <p class="text-gray-600 text-sm">Foco em empresas americanas de alta qualidade que pagam dividendos consistentes.</p>
                    </div>
                    <div class="p-3 rounded-lg bg-gray-50 border">
                        <h3 class="font-bold text-[#3A868C]">AOR</h3>
                        <p class="text-gray-600 text-sm">Alocação de crescimento moderado, balanceando ações e títulos globais (60/40).</p>
                    </div>
                </div>
            </section>

            <section class="lg:col-span-3 md:col-span-2 card rounded-2xl shadow-lg p-6">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">Análise de Ações Brasileiras</h2>
                <p class="text-gray-600 mb-6">Comparativo de indicadores fundamentalistas das ações da sua carteira. Analise a rentabilidade (ROE) em contraste com os múltiplos de mercado (P/L e P/VP) para entender a percepção de valor dos investidores.</p>
                <div class="grid grid-cols-1 xl:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-lg font-semibold text-center text-gray-700 mb-2">Rentabilidade (ROE %)</h3>
                        <div class="chart-container" style="height: 35vh; max-height: 320px;">
                            <canvas id="roeChart"></canvas>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-lg font-semibold text-center text-gray-700 mb-2">Múltiplos de Valuation</h3>
                        <div class="chart-container" style="height: 35vh; max-height: 320px;">
                            <canvas id="valuationChart"></canvas>
                        </div>
                    </div>
                </div>
            </section>

            <section class="lg:col-span-3 md:col-span-2 card rounded-2xl shadow-lg p-6">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">Volatilidade Histórica (Faixa de Preço em 5 Anos)</h2>
                <p class="text-gray-600 mb-6">Este gráfico ilustra a faixa de negociação de cada ativo nos últimos 5 anos. A escala logarítmica permite comparar ativos com ordens de grandeza muito diferentes, como FIIs e Bitcoin, no mesmo gráfico.</p>
                <div class="chart-container" style="height: 60vh; max-height: 550px;">
                    <canvas id="priceRangeChart"></canvas>
                </div>
            </section>
        </main>
    </div>

    <script>
        const wrapLabel = (label, maxLength = 16) => {
            if (typeof label !== 'string' || label.length <= maxLength) {
                return label;
            }
            const words = label.split(' ');
            const lines = [];
            let currentLine = '';
            words.forEach(word => {
                if ((currentLine + ' ' + word).trim().length > maxLength) {
                    lines.push(currentLine.trim());
                    currentLine = word;
                } else {
                    currentLine = (currentLine + ' ' + word).trim();
                }
            });
            if (currentLine) {
                lines.push(currentLine.trim());
            }
            return lines;
        };
        
        const tooltipTitleCallback = (tooltipItems) => {
            const item = tooltipItems[0];
            let label = item.chart.data.labels[item.dataIndex];
            if (Array.isArray(label)) {
              return label.join(' ');
            }
            return label;
        };

        const defaultChartOptions = {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                    labels: { color: '#4A4A4A' }
                },
                tooltip: {
                    callbacks: { title: tooltipTitleCallback }
                }
            },
            scales: {
                y: {
                    ticks: { color: '#6B7280' },
                    grid: { color: '#E5E7EB' },
                    border: { color: '#D1D5DB' }
                },
                x: {
                    ticks: { color: '#6B7280' },
                    grid: { color: '#F3F4F6' },
                    border: { color: '#D1D5DB' }
                }
            }
        };

        const palette = {
            primary: '#3A868C', // Teal
            secondary: '#A2D5D9', // Light Teal
            accent: '#F2C894', // Light Orange
            neutral: '#4A4A4A', // Dark Gray
            background: '#F8F7F4' // Off-white
        };
        
        const chartColors = [palette.primary, palette.secondary, palette.accent, '#88a7b5', '#b2c9d2'];

        new Chart(document.getElementById('portfolioCompositionChart'), {
            type: 'doughnut',
            data: {
                labels: ['Ações Brasileiras', 'ETFs', 'FIIs', 'Criptomoeda'],
                datasets: [{
                    label: 'Nº de Ativos',
                    data: [4, 4, 2, 1],
                    backgroundColor: chartColors,
                    borderColor: palette.background,
                    borderWidth: 4,
                    hoverOffset: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'bottom',
                        labels: { color: palette.neutral, font: { size: 14 } }
                    },
                    tooltip: { callbacks: { title: tooltipTitleCallback } }
                }
            }
        });

        new Chart(document.getElementById('fiiChart'), {
            type: 'bar',
            data: {
                labels: ['GARE11', 'CPTS11'],
                datasets: [{
                    label: 'P/VP',
                    data: [1.01, 0.84],
                    backgroundColor: [palette.primary, palette.secondary],
                    borderColor: '#FFFFFF',
                    borderWidth: 2,
                    borderRadius: 4
                }]
            },
            options: {
                ...defaultChartOptions,
                indexAxis: 'y',
                plugins: { legend: { display: false }, tooltip: { callbacks: { title: tooltipTitleCallback } } }
            }
        });
        
        new Chart(document.getElementById('roeChart'), {
            type: 'bar',
            data: {
                labels: ['CMIG4', 'FIQE3', 'BBAS3', 'DESK3'],
                datasets: [{
                    label: 'ROE (%)',
                    data: [22.84, 14.08, 10.31, 5.79],
                    backgroundColor: palette.primary,
                    borderRadius: 4
                }]
            },
            options: defaultChartOptions
        });

        new Chart(document.getElementById('valuationChart'), {
            type: 'bar',
            data: {
                labels: ['BBAS3', 'CMIG4', 'FIQE3', 'DESK3'],
                datasets: [{
                    label: 'P/L',
                    data: [6.54, 4.89, 8.48, 9.10],
                    backgroundColor: palette.secondary,
                    borderRadius: 4
                }, {
                    label: 'P/VP',
                    data: [0.67, 1.12, 1.19, 0.67],
                    backgroundColor: palette.accent,
                    borderRadius: 4
                }]
            },
            options: defaultChartOptions
        });
        
        const priceRangeData = {
            'CPTS11': [5.47, 10.65], 'GARE11': [7.31, 10.50],
            'BBAS3': [22.17, 55.73], 'CMIG4': [7.00, 15.22],
            'FIQE3': [2.88, 9.45], 'DESK3': [5.97, 26.60],
            'SCHD': [48.10, 82.59], 'AOR': [46.95, 67.17],
            'BOVA11': [61.70, 131.19], 'IVV': [219.28, 528.44],
            'BTC/BRL': [28000, 380000]
        };
        new Chart(document.getElementById('priceRangeChart'), {
            type: 'bar',
            data: {
                labels: Object.keys(priceRangeData),
                datasets: [{
                    label: 'Faixa de Preço (Mín-Máx 5 Anos)',
                    data: Object.values(priceRangeData),
                    backgroundColor: palette.secondary,
                    borderColor: palette.primary,
                    borderWidth: 1,
                    borderRadius: 4
                }]
            },
            options: {
                ...defaultChartOptions,
                indexAxis: 'y',
                scales: {
                    x: {
                        type: 'logarithmic',
                        ticks: { 
                            color: '#6B7280',
                            callback: function(value, index, values) {
                                if (value >= 1000) return (value / 1000) + 'k';
                                return value;
                            }
                        },
                        grid: { color: '#E5E7EB' },
                        border: { color: '#D1D5DB' }
                    },
                    y: {
                        ticks: { color: '#6B7280' },
                        grid: { display: false },
                        border: { color: '#D1D5DB' }
                    }
                }
            }
        });
    </script>
</body>
</html>
