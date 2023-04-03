# Partition Clone : Deep Clone with selected partition

by [Mohit Sauhta](https://www.linkedin.com/in/mohitsauhta)

Oh, I love me some deep clone but we all can use some partition control. Though I do dearly miss Deep Dish from my time in Chicago, but this blog is not about pizza. It is about partition cloning of Delta tables. Let's see how we can do that.

On Databricks platform, the open source delta lake is the foundational layer for the Lakehouse. It is a storage layer that provides ACID transactions, scalable metadata handling, and unifies streaming and batch data processing. It is a great way to store data in a lakehouse. But, what if you want to clone a table with a subset of partitions? Well, you can do that with the help of the delta lake. Let's see how.