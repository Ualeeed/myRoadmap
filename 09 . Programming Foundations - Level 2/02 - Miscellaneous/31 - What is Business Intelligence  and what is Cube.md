---
DATE: 2025-10-26T07:25:00
DONE: true
Name: Foundation 2
---


### **What is Business Intelligence?

Business Intelligence is a collection of technological processes designed to gather, organize, and examine organizational data to produce insights that inform business strategies and operations. *Think of it as a system that helps companies turn raw data into actionable insights.

### **How Does BI Work? (Simple Explanation)

Imagine you run a coffee shop. You have data about:
- How many cups of coffee you sell each day
- Which flavors are most popular
- What times customers visit most
- How much money you make

Business Intelligence tools help you:
1. **Collect** all this information from different sources (cash register, inventory system, etc.)
2. **Organize** it in a way that makes sense
3. **Analyze** it to find patterns
4. **Visualize** it with charts and graphs
5. **Make decisions** based on what you learned

### **The Four Key Steps of BI

<span style="color:rgb(20, 192, 255)">Business intelligence</span> follows four key steps that transform raw data into easy-to-digest insights: data collection, analysis, visualization, and decision-making.

```
Raw Data → Collection → Analysis → Visualization → Decision Making
```

### **Real-World Example

Hershey noticed during the pandemic that people were buying more six-pack chocolate bars and fewer individually-wrapped bars, and that s'mores were becoming popular. Using this intelligence, they adjusted their production and marketing, resulting in an increase of more than $70 million.

### **Benefits of Business Intelligence

BI tools speed up information analysis and performance evaluation, helping companies reduce inefficiencies, flag potential problems, find new revenue streams, and identify areas of future growth.

Key benefits include:
- **Better Decisions**: Based on facts, not guesses
- **Faster Response**: Spot problems quickly
- **Cost Savings**: Find inefficiencies
- **Increased Revenue**: Discover new opportunities
- **Customer Understanding**: Know what customers want

---

## **What is a Cube? (OLAP Cube)

### The Simple Explanation

An OLAP cube is a multi-dimensional array of data that enables computer-based analysis to look for insights. The term "cube" refers to how data is organized in multiple dimensions.

Think of a regular spreadsheet - it has rows and columns (2 dimensions). Now imagine a spreadsheet that has **depth** too - like a Rubik's Cube. That's basically what a data cube is!

### Why "Cube"?

A data cube can be thought of as an extension of the modeling structure provided by a spreadsheet, which accommodates data in rows and columns—a two-dimensional array of data.

**Example:**
- **Dimension 1**: Products (Coffee, Tea, Juice)
- **Dimension 2**: Cities (New York, London, Tokyo)
- **Dimension 3**: Time (January, February, March)

You can quickly answer questions like: "How much coffee did we sell in Tokyo in February?"

### Why Were Cubes Created?

Early BI practitioners realized it was problematic to use SQL databases for large analytical workloads, especially when computer memory was expensive. They developed a solution: extract only needed data from relational databases and store it in an efficient in-memory data structure for manipulation.

### What Can You Do With a Cube?

Conceiving data as a cube with hierarchical dimensions leads to conceptually straightforward operations to facilitate analysis, including slice and dice, drill down, roll up, and pivot operations.

Common operations include:

1. **Slice** - Pick one value for a dimension (e.g., "Show me only 2024 data")
2. **Dice** - Pick specific values from multiple dimensions (e.g., "Show Coffee sales in New York for January")
3. **Drill Down** - Go from summary to detail (e.g., from yearly to monthly sales)
4. **Roll Up** - Go from detail to summary (e.g., from daily to monthly totals)
5. **Pivot** - Rotate the view to see data from different angles

### Modern Reality: Are Cubes Still Used?

Today, most BI teams run OLAP workloads on columnar databases in the cloud rather than creating data cubes as a separate layer, thanks to three developments: the power and scalability of cloud data warehouses, the flexibility of modern data pipeline tools, and how cloud-native analytics tools connect directly to data sources.

**In short**: Traditional cubes are becoming less common because cloud technology now allows us to analyze data directly without needing the cube structure. However, the **concept** of multi-dimensional analysis is still very important!

---

## How BI and Cubes Work Together

```mermaid
graph LR
    A[Raw Data Sources] --> B[Data Collection]
    B --> C[Data Warehouse]
    C --> D[OLAP Cube / Analysis]
    D --> E[BI Tools & Dashboards]
    E --> F[Business Decisions]
```

1. **Data Sources**: Sales records, customer data, inventory, etc.
2. **Collection**: Gather and clean the data
3. **Storage**: Put it in a data warehouse
4. **Analysis**: Use cubes or modern tools to analyze
5. **Visualization**: Create charts and dashboards
6. **Action**: Make informed business decisions

---

## Key Takeaways

### Business Intelligence:
- Helps companies make **data-driven decisions**
- Transforms raw data into **meaningful insights**
- Uses tools for **visualization** and **reporting**
- Answers questions like "What happened?" and "Why?"

### OLAP Cube:
- A **multi-dimensional data structure** for fast analysis
- Allows you to **slice, dice, and pivot** data
- Originally created when computer memory was expensive
- Being replaced by modern cloud-based solutions but the concepts remain important

### The Big Picture:
<span style="color:rgb(181, 75, 251)">BI</span> is the overall process of turning data into insights. <span style="color:rgb(181, 75, 251)">Cubes</span> were a specific technology used within BI systems to make analysis faster. Today, cloud computing gives us new and better ways to do the same thing, but understanding cubes helps you understand how data analysis works!

---

## Further Learning

If you're interested in BI and data analysis, consider learning:
- SQL for querying databases
- Data visualization tools (Tableau, Power BI, Excel)
- Python or R for data analysis
- Cloud data warehouses `(Snowflake, BigQuery, AWS Redshift)`
- Basic statistics and data analysis concepts