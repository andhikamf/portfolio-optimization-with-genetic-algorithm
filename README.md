# Portfolio Optimization using Genetic Algorithm

Optimasi portofolio saham menggunakan **Genetic Algorithm (GA)** untuk mencari alokasi bobot yang memaksimalkan trade-off antara return dan risiko.  
Studi kasus menggunakan saham perbankan Indonesia: **BBRI, BMRI, dan BBCA**.

kenapa big banks? simpelnya liquid dan harga ga gampang digoreng.
## Overview
Project ini mengeksplorasi pendekatan **evolutionary optimization** untuk masalah alokasi aset.  
GA dipakai karena lebih fleksibel menghadapi market yang non-linear dan noisy.

Objective yang dioptimalkan:

Mirip Sharpe Ratio, tapi **tanpa risk-free rate**.

## Data
- **Assets**: BBRI.JK, BMRI.JK, BBCA.JK  
- **Period**: January 2021 – January 2023  
- **Source**: Yahoo Finance (`yfinance`)  
- **Processing**:
  - Harga penutupan harian
  - Dikonversi menjadi return bulanan (compounded)

Return bulanan digunakan untuk mengurangi noise dan membuat proses optimasi lebih stabil.

## Methodology

### Portfolio Metrics
- **Expected Return**: rata-rata return bulanan
- **Volatility**: dihitung dari covariance matrix
- **Fitness**: return / volatility

### Genetic Algorithm Setup
- Population size: 80  
- Generations: 50  
- Selection: tournament selection  
- Crossover: one-point crossover  
- Mutation: Gaussian noise  
- Elitism: top 4 individuals  

Constraints:
- Bobot ≥ 0 (no short selling)
- Total bobot = 1 (fully invested)

## Baseline Comparison
Hasil GA dibandingkan dengan:
1. **Equal Weight Portfolio** (1/N, N = total saham di dalam portofolio)
2. **Best Single Stock Strategy** (all in di saham dengan return rata-rata tertinggi)

Tujuannya untuk melihat apakah GA benar-benar memberikan peningkatan performa dibanding strategi sederhana.

## Results
Evaluasi dilakukan menggunakan:
- Average monthly return
- Volatility
- Risk-adjusted return (fitness)

Visualisasi yang dihasilkan:
- Perkembangan fitness GA per generasi
  <img width="1051" height="573" alt="image" src="https://github.com/user-attachments/assets/82c9f00b-fb10-4225-917a-295cd5f5f651" />

- Perbandingan return dan volatilitas antar metode
  <img width="832" height="548" alt="image" src="https://github.com/user-attachments/assets/5a8236f4-6c77-4414-a83d-ad47bccaf3b7" />
  <img width="815" height="539" alt="image" src="https://github.com/user-attachments/assets/a06da06e-96ef-4f01-ba1b-1f8c456ce4d4" />

- Alokasi bobot optimal
  <img width="714" height="682" alt="image" src="https://github.com/user-attachments/assets/3925b9e0-c521-4c40-81af-6d28235a5d28" />

- Time series return bulanan portofolio
  <img width="1136" height="544" alt="image" src="https://github.com/user-attachments/assets/3cb14102-7bed-45a5-b9cb-acece07a53e9" />


Secara umum, GA menghasilkan alokasi yang lebih seimbang dan risk-adjusted return yang lebih stabil dibanding baseline.

## Limitations
- Tidak menggunakan risk-free rate
- Tidak memperhitungkan transaction cost
- Tidak ada rebalancing periodik
- Genetic Algorithm bersifat stochastic (hasil bisa berbeda setiap run)

(masih pemula bang😅)
## Possible Improvements
- Menambahkan risk-free rate
- Rolling window optimization dan rebalancing
- Perbandingan langsung dengan Markowitz optimization
- Penambahan constraint (max weight, sector cap)
- Eksplorasi algoritma lain seperti PSO atau Differential Evolution


## Tech Stack
- Python
- NumPy
- Pandas
- Matplotlib
- yFinance


## Notes
Project ini dibuat sebagai eksplorasi optimasi portofolio dan evolutionary algorithms.  
Fokus utama ada pada **framework, reasoning, dan evaluasi risiko**, bukan nyari strategi “pasti profit”.

Market itu noisy, so please DYOR😁.
