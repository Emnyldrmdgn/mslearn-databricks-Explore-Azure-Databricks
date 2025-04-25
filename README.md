# mslearn-databricks-Explore-Azure-Databricks
Azure Databricks is a Microsoft Azure-based version of the popular open-source Databricks platform.  An Azure Databricks workspace provides a central point for managing Databricks clusters, data, and resources on Azure.
# 🚀 Getting Started with Azure Databricks

This guide walks you through setting up an Azure Databricks workspace, creating a Spark cluster, uploading a CSV file, running SQL and PySpark queries, and cleaning up your resources.

---

## 1. 🚀 Create an Azure Databricks Workspace

> If you already have a workspace, you can skip this step.

In the [Azure Portal](https://portal.azure.com):

- Sign in and create a new **Azure Databricks** resource.
- Use the following settings:
  - **Subscription**: Your active Azure subscription
  - **Resource Group**: `msl-xxxxxxx` (use a unique name)
  - **Workspace Name**: `databricks-xxxxxxx`
  - **Region**: Any available region
  - **Pricing Tier**: Premium or Trial
  - **Managed Resource Group**: `databricks-xxxxxxx-managed`

✅ Click **Review + create**, then **Create**. Once deployment is complete, click **Go to resource** → **Launch Workspace**.

---

## 2. 🧩 Create a Cluster

A cluster is required to run Spark jobs.

Once inside the Databricks Workspace:

- On the left menu, click **+ New** → **Cluster**
- Use the following settings:
  - **Cluster Name**: (Leave the default name)
  - **Policy**: Unrestricted
  - **Cluster Mode**: Single Node
  - **Access Mode**: Single User
  - **Runtime Version**: 13.3 LTS (Spark 3.4.1)
  - **Use Photon**: Enabled
  - **Node Type**: Standard_D4ds_v5
  - **Terminate after inactivity**: 20 minutes

📌 **Note**: If the cluster fails to start, check your region’s CPU core quota or try a different region.

---

## 3. 📂 Upload CSV and Query with SQL

1. Download the `products.csv` file from:  
   [https://raw.githubusercontent.com/MicrosoftLearning/mslearn-databricks/main/data/products.csv](https://raw.githubusercontent.com/MicrosoftLearning/mslearn-databricks/main/data/products.csv)

2. In Databricks Workspace:
   - Click **+ New** → **Add or upload data**
   - Upload the `products.csv` file

3. In the **Create table** page:
   - **Catalog**: `hive_metastore`
   - **Schema**: `default`
   - **Table Name**: `products`

4. Once the table is created:
   - Click **Create** → **Notebook**
   - Run the default SQL code in the first cell:
     ```sql
     %sql
     SELECT * FROM hive_metastore.default.products;
     ```

5. To visualize results:
   - Click **+** above the result table → **Visualization**
   - **Type**: Bar
   - **X**: Category
   - **Y**: ProductID (Aggregation: Count)

---

## 4. 🐍 Analyze Data with PySpark

Add a new code cell below the chart and enter the following:

``python
df = spark.sql("SELECT * FROM products")
df = df.filter("Category == 'Road Bikes'")
display(df)

## 5. 🧹 Clean Up Resources
In the Compute page, select your cluster and click Terminate.
Optionally, go back to the Azure Portal and delete the entire resource group to remove all associated resources.

## Screenshots

![lab1databricks](https://github.com/user-attachments/assets/35fca2bb-0751-4c1a-9ee0-e62d79912a97)
![lab1databricks3](https://github.com/user-attachments/assets/f470fea9-971c-4428-aeb8-0bdcdaed1d03)
![lab1databricks2](https://github.com/user-attachments/assets/a0eebcf3-982d-4e59-93f4-50ef9bd12c20)
![lab1databricks4](https://github.com/user-attachments/assets/d4c7ce71-e3e8-4b2c-8f5a-c54d02651659)
![lab1databricks5](https://github.com/user-attachments/assets/080a1d41-7f5e-4c93-b1fd-326092d33c7a)
![lab1databricks6](https://github.com/user-attachments/assets/663c0bd1-3214-41d3-a855-9afa4795647b)
![lab1databricks6-2](https://github.com/user-attachments/assets/592c1123-b806-4026-9f8d-e4dc1f49fb4b)
![lab1databricks6-3](https://github.com/user-attachments/assets/52f5dae2-92ec-4db5-b2aa-9801db882caa)
![lab1databricks7](https://github.com/user-attachments/assets/40a96d52-885a-476b-8f08-d28fc768373e)

