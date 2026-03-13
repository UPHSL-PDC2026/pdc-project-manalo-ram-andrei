# **Technical Report**

## **Problem Description**

The objective of this study was to analyze a diabetes dataset containing patient records, including attributes such as **age, gender, BMI, blood glucose level, and diabetes status**. The goal was to compare sequential and parallel processing approaches in terms of execution time, speedup, and efficiency. The specific tasks were to:

- Filter records to identify patients with diabetes.
- Compute the average blood glucose level for the diabetic patients.
- Identify the top 10 patients with the highest BMI.

---

## **Parallelization Approach**

The parallelization was implemented using Python’s **multiprocessing** module:

**Data Chunking:** The dataset was filtered for diabetic patients and split into chunks, one per available CPU core. This ensures that each process works on a roughly equal portion of the dataset, which also helps balance the computational workload.

**Chunk Processing:** Each chunk was processed independently in parallel using **Pool.map()**, computing the mean blood glucose, count, and top 10 BMI records. Processing the chunks all at the same time helps in reducing the execution time compared to sequential processing especially for large datasets.

**Result Aggregation:** The results from all chunks were combined to compute the overall mean glucose and the top 10 BMI records across all chunks. Aggregation is very crucial as it is done to avoid missing any records, which ensures that the output is accurate and reliable.

---
