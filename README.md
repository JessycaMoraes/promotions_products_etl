# 📊 Promotions & Products – ETL Pipeline

## 🌐 Overview
This project implements an ETL (Extract, Transform, Load) pipeline using Google Colab to process a dataset of products and promotions.

The data is cleaned, transformed, and loaded into Google BigQuery, providing a structured and reliable foundation for analysis and dashboarding in Looker Studio.

⚠️ Note: This project was developed as part of a technical assessment based on a fictional business scenario.

---

## 🛠️ Tech Stack
- 🐍 Python (Google Colab)
- ☁️ Google BigQuery
- 📊 Looker Studio
- 📦 Pandas, NumPy, Matplotlib, Seaborn

---

## 📊 Interactive Dashboard
[![Dashboard View](promotions_products_logo.png)](https://datastudio.google.com/s/oMKxxy-FiKo)

🔗 Click on the image above or access it directly via the link: 
[https://datastudio.google.com/s/oMKxxy-FiKo](https://datastudio.google.com/s/oMKxxy-FiKo)

---

## 📚 Data Dictionary

This data dictionary describes the structure of the dataset used in the ETL pipeline.

| Column | Description |
|--------|------------|
| cod_ciclo | Product cycle identifier |
| cod_ano | Cycle year |
| cod_canal | Sales channel |
| cod_agrupador_sap_material | Product ID |
| cod_regional_agrupador | Product region code |
| cod_uf | State |
| des_categoria_material | Product category |
| des_subcategoria_material | Product subcategory |
| des_marca_material | Product brand |
| des_tier | Product price range |
| des_mecanica_consumidor | Promotion description for the consumer |
| des_mecanica_rev | Promotion description for the reseller |
| des_promocao_publico | Target audience of the promotion |
| vlr_desconto_real | Total discount value applied |
| vlr_rbv_ta-bela_so_tt | Total listed revenue (before discounts) |
| vlr_rbv_real_so_tt | Total actual revenue |
| vlr_preco_base | Base unit price (full/list price) |
| vlr_preco_venda | Actual unit selling price |
| vlr_preco_tabela | Listed unit price (full price) |
| vlr_desconto_real2 | Discount value applied per product |

---

## 📥 Data Extraction
- Source: CSV dataset (local project file)
- Initial load using `pandas.read_csv()`
- Records: 19,502  
- Columns: 20  

---

## 🧹 Data Transformation

### 🔹 Duplicate Removal
- 200 duplicate rows removed  
- Final dataset: 19,302 records  

### 🔹 Missing Values Handling
- `vlr_desconto_real` and `vlr_desconto_real2`: filled with median  
- `cod_ano`: derived from `cod_ciclo`  

### 🔹 Data Type Adjustments
- `cod_agrupador_sap_material`: converted from float to string  

### 🔹 Categorical Variables
- No columns with >90% dominance → all retained  

### 🔹 Outlier Analysis
- Detected using IQR method  
- Outliers were **kept**, as they may represent real promotional strategies  

---

## 📈 Exploratory Data Analysis
- Descriptive statistics  
- Boxplots and visual inspection  
- Identification of pricing and discount patterns  

---

## ☁️ Data Loading (BigQuery)
- Authentication via service account  
- Explicit schema definition using `SchemaField`  
- Load method: `WRITE_TRUNCATE`  

```python
job = client.load_table_from_dataframe(
    df_prom_prod, 
    table_ref, 
    job_config=job_config
)
```

---

## 🗺️ Output & Insights
- Clean and structured dataset in BigQuery
- Ready for BI consumption
- Supports decision-making through dashboards

---

## ✅ Key Outcomes
- Reliable ETL pipeline
- Improved data quality and consistency
- Scalable structure for analytics

---

## 📄 Business Presentation

This project also includes a business-oriented presentation with key insights and strategic recommendations.

📥 [Download Presentation](./presentation_en.pdf)

---

## 🚀 Next Steps
- Add data validation layers
- Implement incremental loads
- Enhance dashboard with business KPIs

---

> ⚠️ *“based on a fictional business scenario”*