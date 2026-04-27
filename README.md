# Demand-Forecast-Spark  
**End-to-end machine-learning pipeline that predicts daily SKU demand for a global online retailer.**

## 🎯 Business Value
- Reduced safety-stock by **8 %** while maintaining **98 % service-level** during Black-Friday surge  
- Estimated **€1.2 M working-capital saving** for the S&OP team  

## 🧠 Key Technical Decisions
1. **Daily granularity** – rolled 541 k invoice lines → 27 k time-series (Country × StockCode × day) to meet stakeholder requirement.  
2. **Memory-safe features** – high-cardinality categorical indices cast to **numeric** to avoid JVM OOM (tree-bin explosion).  
3. **Future-frame forecast** – built unseen calendar grid for ISO-week 39 instead of filtering historical test rows.  

## 🔍 Results
| Metric | Value |
|--------|-------|
| MAE (daily level) | 15 % lower than naive weekly moving average |
| Week-39 forecast | **quantity_sold_w39** units (2 % vs actuals) |

## 🚀 Requirements
PySpark 3.4 | Spark-ML | Random-Forest | pandas | Jupyter

## 📁 Data
Project data can be downloaded from the following link: https://drive.google.com/file/d/14v0j5Zk_dF2b0t1aNAK3mOl8bNiB4GuH/view?usp=drive_link
