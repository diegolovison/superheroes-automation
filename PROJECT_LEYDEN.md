# Project Leyden: Performance Definitions & Training Workflow

Based on the presentation *"P[roject Leyden's AOT - Shifting Java Startup into High Gear](https://www.youtube.com/watch?v=Oo96adJirPw)"*.

### **Core Performance Metrics**

Project Leyden is about improving the *startup* and *warmup* of Java applications.

* **Startup**
  Defined as the time it takes to get to the first useful unit of work.

* **Warmup**
  Defined as the time it takes for the application to reach peak performance.

---

### **The Training Run**

*Note: This concept is different from the presentation. The presentation is suggesting from observing a production workload or creating an integration test.*

*Note: This definition outlines a specific checkpoint-based workflow for generating and utilizing optimization artifacts.*

A **Training Run** is a preparatory execution phase used to capture the application's behavior and state before production deployment. This process follows a cyclical validation pattern:

1. **Initial Warmup:** A load generator executes a benchmark against the application for a specified duration to exercise code paths.
2. **Artifact Generation:** The application state is captured, and a checkpoint (containing optimization artifacts and heap state) is stored.
3. **Restoration:** The application is restored from the saved checkpoint (utilizing the stored artifacts).
4. **Validation:** The load generator runs the benchmark again against the restored application to ensure peak performance is achieved immediately.

---

### **Going to Production**

Once the Training Run is complete, the artifacts are evaluated for deployment suitability:

* **Condition:** If the validation in step 4 confirms that the restored application meets performance thresholds (immediate startup and peak throughput).
* **Promotion:** The specific **Checkpoint** generated in step 2 is promoted to the production environment.
* **Result:** Production instances start directly from this optimized state, effectively skipping the startup and warmup phases experienced during the Initial Warmup.