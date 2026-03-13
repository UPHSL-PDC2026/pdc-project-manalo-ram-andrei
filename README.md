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

## **Challenges Encountered**

- **Jupyter Not Working:** The main challenge we faced in this project was the actual execution of the parallel processing. Initially, we used Jupyter in running the code, but every time it comes to parallel processing code, the cell never completes and just runs infinitely. We tried to fix the code for the parallel section and unfortunately, the problem still exists. But when we switched to Google Colab, it immediately worked out fine and the parallel processing was executed without any errors. The disparity in performance occurs because Google Colab operates on a Linux-based environment that uses the fork method to create instant memory copies for worker processes, whereas local Windows or macOS Jupyter instances use the more resource-heavy spawn method. This local "spawn" approach requires a clean re-import of the entire script for every CPU core, which often triggers deadlocks or infinite loops if the notebook structure isn't perfectly isolated. Consequently, Colab’s streamlined process management avoids the "zombie processes" and memory overhead that cause local machines to hang during intensive data pickling.

- **Limited CPU Cores:**  Yhe program ran only on a system with only 2 processors, which limited the potential speedup of the program. Parallel processing is known to work better with a higher number of processors.  

- **Overhead of Multiprocessing:** Since the dataset we used was relatively small, the spawning of multiple processes and managing the communication between these processes led to a slower execution time. Parallel processing works better with larger datasets to maximize the chunk management.

---
## **Project Overview**

This project analyzes a diabetes dataset to identify patients with diabetes, calculate their average blood glucose levels, and determine the top 10 patients with the highest BMI. The project compares sequential and parallel data processing methods to evaluate performance differences and understand the benefits and limitations of parallelization.

---

## **Tools and Technologies Used**

- **Programming Language:** Python 3.13.7  
- **Libraries:**  
  - pandas – for data manipulation and analysis  
  - multiprocessing – for parallel computation  
  - time – to measure execution performance  
- **Development Environment:** Google Colab  
- **Dataset:** diabetes_dataset.csv containing patient demographics, medical history, and lab results
