# Data Quality simplified with Spark and Data Grading made possible with Delta Lake

by  [Nav Alam](https://www.linkedin.com/in/navdeepalam/), [Mohit Sauhta](https://www.linkedin.com/in/mohitsauhta/?lipi=urn%3Ali%3Apage%3Ad_flagship3_feed%3Bjtf%2BJ3jHT5e7zyeq9hpuqA%3D%3D)

```
This is collaborative work from Abacus Insights and Beesbridge, the delivery partner for Databricks.
```

Data quality (DQ) is a critical component of any data-driven organization and one of the pillars for effective Data Governance. In traditional settings, the data quality captures the following dimensions about the data: Accuracy, Completeness, Consistency, and Timeliness. Abacus Insights, as an Innovative Data Platform provider that push the bounds of legacy data management platforms,  needs to deal with the realities of integrating data silos, where eventual consistency is guaranteed, but may not be available in real-time. We introduce a concept of **Data Grading** where the data carries along with the data quality score. The natural corrollary about that score is to have **Process Transparency** so our customers can interpret those results. This blog post will walk you through the high level details of how we have implemented these concepts using Spark engine, and Delta Lake on the Databricks platform.

Abacus Insights manages healthcare data by breaking down data silos to make a real impact for our customers. Our platform standardizes data across the healthcare ecosystem by providing a highly secure unified data infrastructure that minimizes change management and maximizes analytics enablement to reduce costs and improve outcomes. We provide a data platform that enables our customers to build a data-driven culture and drive better outcomes.


## Process Transparency
Data grading is the outcome of data quality rules that can be applied on the raw data from source system in `Bronze` layer, as well as the data which is transformed and enriched in `Silver` layer. The section explores the construction of data quality grammar that enables business user to interpet the DQ rule, as well as the runtime deployment of those rules in cost efficient manner.

### Data Quality Grammar
First question that comes to mind is why do we need a grammar for data quality rule?  The less rigorous answer is that the grammar can be customized to represent the opinionated version of the narrow domain.  On other hand, one can also build such rules in one of the popular data quality tools/libraries - after all, these tools provide rich visual interface and even platform agnostic integration to protect investments against the platform changes.However, these tools are not designed to work natively on the Databricks platform that support co-mingled workload: Batch and Streaming data.  In addition, these tools are not custom built for delta lakehouse use cases. The grammar is not only designed to be a simple and intuitive way to express the data quality rules, but also to produce efficient code that can be run natively using Dataframe along with the data engineering pipelines.  

The grammar is constructed using the following components:
1. DQ Grammar : Used to state the domain specific language for data quality rules.
2. DQ Rules  : Used to define the data quality rules.
3. DQ Parser : Used to parse the data quality rules, and generate the effective data quality rules.

 