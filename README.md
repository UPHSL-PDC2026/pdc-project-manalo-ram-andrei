# **Technical Report**

## **System Architecture Diagram**

The system architecture for this project follows a layered approach consisting of data input, processing, and output components. At the input layer, the dataset is loaded from a CSV file into different processing environments, including pandas for sequential execution, multiprocessing for parallel execution, and Apache Spark for distributed processing. Each environment serves as a separate execution model, which allows for direct comparison of performance and scalability across implementations.

The processing layer handles the data analytics, including filtering records with diabetes, computing the average blood glucose level, and retrieving the top 10 records based on BMI. In the distributed execution, Apache Spark divides the dataset into partitions and processes them across worker nodes, enabling parallel computation at scale. Finally, the output layer consolidates the results and presents them through printed outputs and comparison tables, which enables evaluation of execution time across all approaches.

<img width="1120" height="1520" alt="PDC" src="https://github.com/user-attachments/assets/c404e066-ae7a-4d23-87a3-7b8e47f7981b" />


## **Performance Evaluation**

The project’s performance evaluation shows that the sequential implementation achieved the fastest execution time with approximately 0.0065 seconds, followed by the parallel execution with 0.061 seconds, while the distributed execution using Apache Spark recorded the slowest performance with 2.45 seconds. This result happened due to the relatively small dataset size that was used, which only contains 100,000 rows, and the simplicity or uncomplicated operations performed on the data, such as filtering, averaging, and sorting. Because of this, the overhead that came from the multiprocessing and distributed performance outweighed the computational benefits, which led to slower execution times. 

Despite the slower execution time in this project, the distributed approach shows its potential for handling large amounts of data and processing tasks. The additional overhead that comes from using Apache Spark can become justified and more helpful when we work with significantly larger datasets or more complex analytical tasks and operations. In conclusion, while sequential processing is optimal for small datasets like in this project, distributed computing still remains essential in big data environments.

## **Scalability Benefits and Limitations**

Distributed computing frameworks such as Apache Spark provide significant scalability benefits by allowing data processing to be distributed across multiple nodes. This enables the system to handle large datasets efficiently by dividing the workload into smaller partitions that can be processed in parallel. As data volume increases, additional computational resources can be added to maintain performance, making distributed systems highly suitable for big data applications and real-time analytics.

However, this scalability comes with certain limitations, particularly for small datasets like the one used in this project. The overhead associated with initializing distributed systems, managing task scheduling, and coordinating between nodes can negatively impact the performance when the workload is not relatively large. In this project, the dataset size was not large enough to benefit from distributed processing, which resulted in slower execution times compared to the sequential approach. This highlights that scalability benefits are highly dependent on the size and complexity of the data being processed.


## **Ethical and Professional Considerations**

The use of health-related datasets, such as diabetes records, raises important ethical considerations regarding data privacy and responsible usage. Even though the dataset used in this project does not include personally identifiable information, it is important to ensure that sensitive health data is handled securely and stored properly. Unauthorized access or misuse of such data can lead to privacy violations and ethical concerns, which emphasizes the need for secure data storage and controlled access.

In addition, responsible data usage requires careful interpretation of results to avoid bias or misleading conclusions. Factors such as gender, age, or location should not be used to generalize or discriminate against specific groups. Analysts must ensure that insights derived from the data are used ethically and for beneficial purposes, such as improving healthcare outcomes or informing research. Maintaining transparency, fairness, and accountability in data processing is essential in upholding professional standards in data science and computing.


## **Problem Description**

The objective of this study was to analyze a diabetes dataset containing patient records, including attributes such as **age, gender, BMI, blood glucose level, and diabetes status**. The goal was to compare sequential and parallel processing approaches in terms of execution time, speedup, and efficiency. The specific tasks were to:

- Filter records to identify patients with diabetes.
- Compute the average blood glucose level for the diabetic patients.
- Identify the top 10 patients with the highest BMI.

---

## **Parallelization Approach**

The parallelization was implemented using Python’s **multiprocessing** module:

**Data Chunking:** The dataset was filtered for diabetic patients and split into chunks, one per available CPU core. This ensures that each process works on a roughly equal portion of the dataset, which also helps balance the computational workload.

**Chunk Processing:** Each chunk was processed independently in parallel using **Pool.map()**, computing the mean blood glucose, count, and top 10 BMI records. Processing the chunks all at the same time helps in reducing the execution time compared to sequential processing, especially for large datasets.

**Result Aggregation:** The results from all chunks were combined to compute the overall mean glucose and the top 10 BMI records across all chunks. Aggregation is very crucial as it is done to avoid missing any records, which ensures that the output is accurate and reliable.

---

## **Performance Analysis**

- Sequential Execution Time = 0.0079 seconds  
- Parallel Execution Time = 0.0697 seconds  
- Speedup = 0.11 (Sequential time / Parallel time)  
- Number of Processors = 2  
- Efficiency = 0.057 (Speedup / Number of processors)  

The sequential version of the program executed quickly at only 0.0079 seconds, while the parallel version took approximately 0.0697 seconds. The reason why sequential execution time is faster is because the dataset was relatively small with 100,000 rows. Another reason for the slower execution time of the parallel version is the overhead it experienced with parallel processing. This includes creating multiple processes and distributing the data chunks, which will benefit a larger dataset more than a small one.

The calculated speedup is 0.11, while the efficiency is 0.057, which indicates that the system is not using the available cores effectively. However, if the dataset was larger, the parallelization could definitely be more useful in reducing the execution time. This shows that parallel processing is not always faster. It depends also on the workload that needs to be done and the overhead of managing multiple processes.

---

## **Challenges Encountered**

- **Jupyter Not Working:** The main challenge we faced in this project was the actual execution of the parallel processing. Initially, we used Jupyter in running the code, but every time it comes to parallel processing code, the cell never completes and just runs infinitely. We tried to fix the code for the parallel section and unfortunately, the problem still exists. But when we switched to Google Colab, it immediately worked out fine and the parallel processing was executed without any errors. The disparity in performance occurs because Google Colab operates on a Linux-based environment that uses the fork method to create instant memory copies for worker processes, whereas local Windows or macOS Jupyter instances use the more resource-heavy spawn method. This local "spawn" approach requires a clean re-import of the entire script for every CPU core, which often triggers deadlocks or infinite loops if the notebook structure isn't perfectly isolated. Consequently, Colab’s streamlined process management avoids the "zombie processes" and memory overhead that cause local machines to hang during intensive data pickling.

- **Limited CPU Cores:**  The program ran only on a system with only 2 processors, which limited the potential speedup of the program. Parallel processing is known to work better with a higher number of processors.  

- **Overhead of Multiprocessing:** Since the dataset we used was relatively small, the spawning of multiple processes and managing the communication between these processes led to a slower execution time. Parallel processing works better with larger datasets to maximize chunk management.

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

---

## **Instructions for Running the Project**

1. **Install Dependencies:** Ensure Python 3.7+ is installed along with the required libraries.  
2. **Place Dataset:** Ensure the diabetes_dataset.csv file is in the same directory as the Python script or notebook.  
3. **Run Sequential Code:** Execute the sequential computation function to see average glucose levels and top 10 BMI records.  
4. **Run Parallel Code:** Execute the parallel computation function to see results computed using multiprocessing.  
5. **Compare Performance:** Execution times, speedup, and efficiency are printed automatically for comparison.

## **Project Team**

| **Name**       | **Role**                          |
|----------------|----------------------------------|
| Follante, Adrian Paolo S.    | Project Lead / Python Developer  |
| Manalo, Ram Andrei M.    | Data Analyst / Dataset Preparation / Documentation |
| Ramos, Renzo Emmanuel V.    | Python Developer / Report Writer / Documentation     |
| Rivera, France Raphael S.   | Testing & Performance Evaluation  |
| Torculas, Richard O.   | Report Writer / Documentation  |

