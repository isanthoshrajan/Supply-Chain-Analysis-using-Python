# Supply-Chain-Analysis-using-Python
Conducted supply chain analysis using Python to evaluate demand, inventory, logistics, and supplier performance. Identified revenue drivers, cost inefficiencies, and defect patterns across transportation modes. Generated actionable insights to optimize operations, reduce costs, and improve overall supply chain efficiency.

### Project Overview

This project analyzes supply chain data of a fashion and beauty business to identify inefficiencies in operations, including demand patterns, inventory management, supplier performance, and logistics. The goal is to uncover actionable insights that can improve operational efficiency and reduce costs.

### Project Objectives

- Analyze product demand and revenue trends
- Evaluate inventory and stock levels
- Identify delays in shipping and delivery
- Assess supplier and transportation performance
- Analyze defect rates across supply chain stages

### Dataset Description

The dataset contains supply chain data including:

- Product information (SKU, product type, price)
- Sales and revenue details
- Inventory and stock levels
- Lead times and production data
- Shipping carriers and transportation modes
- Defect rates and operational costs

Each row represents a product-level supply chain record.

### Data Dictionary

| Column Name | Description |
|------------|------------|
| Product type | Category of product (haircare, skincare, cosmetics) |
| SKU | Unique product identifier |
| Price | Product price |
| Availability | Product availability level |
| Number of products sold | Units sold |
| Revenue generated | Revenue from product |
| Customer demographics | Customer segment |
| Stock levels | Inventory quantity |
| Lead times | Delivery lead time |
| Order quantities | Quantity ordered |
| Shipping times | Time taken to ship |
| Shipping carriers | Carrier used |
| Manufacturing costs | Cost of production |
| Defect rates | Percentage of defective products |
| Transportation modes | Mode (Air, Road, Rail) |
| Costs | Transportation cost |

### Tools Used
Python — Data analysis
Pandas — Data manipulation
Plotly — Interactive visualization

### Analysis & Key Insights

## 1. Price vs Revenue Analysis
```python
fig = px.scatter(data, x='Price', 
                 y='Revenue generated', 
                 color='Product type', 
                 hover_data=['Number of products sold'], 
                 trendline="ols")
fig.show()
```
**Output:**

<img width="1065" height="390" alt="Price vs Revenue Analysis" src="https://github.com/user-attachments/assets/2957fee2-972d-410d-a283-bcd12a03b95b" />


Insight: Higher-priced skincare products generate more revenue, indicating strong demand in this segment.

## 2. Sales Distribution by Product Type
```python
sales_data = data.groupby('Product type')['Number of products sold'].sum().reset_index()

pie_chart = px.pie(sales_data, values='Number of products sold', names='Product type', 
                   title='Sales by Product Type', 
                   hover_data=['Number of products sold'],
                   hole=0.5,
                   color_discrete_sequence=px.colors.qualitative.Pastel)
                   
pie_chart.update_traces(textposition='inside', textinfo='percent+label')
pie_chart.show()
```
**Output:**
<img width="1102" height="375" alt="Sales Distribution by Product Type" src="https://github.com/user-attachments/assets/257109a9-ab9d-4f9c-977d-10515b16c300" />

Insight: Skincare contributes the highest share of sales (~45%), making it the dominant product category.

## 3. Revenue by Shipping Carrier
```python
total_revenue = data.groupby('Shipping carriers')['Revenue generated'].sum().reset_index()
fig = go.Figure()
fig.add_trace(go.Bar(x=total_revenue['Shipping carriers'], 
                     y=total_revenue['Revenue generated']))
fig.update_layout(title='Total Revenue by Shipping Carrier', 
                  xaxis_title='Shipping Carrier', 
                  yaxis_title='Revenue Generated')
fig.show()
```
**Output:**
<img width="1102" height="360" alt="Revenue by Shipping Carrier" src="https://github.com/user-attachments/assets/cb35ca4e-4749-4946-948e-8839bb25b4c9" />


Insight: Carrier B generates the highest revenue but may also involve higher operational costs.

## 4. Cost Distribution by Transportation Mode
```python
transportation_chart = px.pie(data, 
                              values='Costs', 
                              names='Transportation modes', 
                              title='Cost Distribution by Transportation Mode',
                              hole=0.5,
                              color_discrete_sequence=px.colors.qualitative.Pastel)
transportation_chart.show()
```
**Output:**
<img width="1079" height="360" alt="Cost Distribution by Transportation Mode" src="https://github.com/user-attachments/assets/63e8c0de-3789-413a-ad41-69421645e618" />


Insight: Road and Rail transportation account for the majority of logistics costs.

## 5. Defect Rate by Transportation Mode
```python
pivot_table = pd.pivot_table(data, values='Defect rates', 
                             index=['Transportation modes'], 
                             aggfunc='mean')

transportation_chart = px.pie(values=pivot_table["Defect rates"], 
                              names=pivot_table.index, 
                              title='Defect Rates by Transportation Mode',
                              hole=0.5,
                              color_discrete_sequence=px.colors.qualitative.Pastel)
transportation_chart.show()
```

**Output:**
<img width="1102" height="360" alt="newplot" src="https://github.com/user-attachments/assets/4ffb6c2d-222e-4449-b46d-7a14f36f4b6e" />

Insight: Road transportation shows higher defect rates, while Air transport is more reliable.

### Key Findings
- Skincare products drive the highest revenue and demand
- Carrier B contributes most revenue but increases cost burden
- Inventory and SKU performance vary significantly
- Road transport leads to higher defect rates
- Haircare products show quality-related issues

### Business Recommendations
- Optimize product pricing strategy for high-demand categories
- Evaluate cost vs benefit of shipping carriers
- Reduce dependency on high-defect transportation modes
- Improve quality control for high-defect product categories
- Optimize inventory based on SKU performance

 ### Conclusion

This project demonstrates how supply chain data can be analyzed using Python to uncover inefficiencies and optimize operations. By analyzing demand, logistics, and defect rates, businesses can make data-driven decisions to improve performance and reduce costs. 





