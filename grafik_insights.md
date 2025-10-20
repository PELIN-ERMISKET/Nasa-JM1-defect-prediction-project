## 📊 Graph Analysis Summary ##

    This study presents graphical evaluations supporting the data analysis process conducted on the NASA JM1 Software Defect Prediction Dataset.
The visualizations illustrate the relationships between various software metrics and defect presence, highlighting key patterns and trends.
This file contains insights and observations derived from each plotted figure.

## Correlation Heatmap Analysis

![Correlation Heatmap Analysis](Images/Correlation_Heatmap_of_Software_Metrics.png)

The correlation heatmap provides a comprehensive view of how software complexity metrics relate to one another and to the defects variable within the NASA JM1 dataset.

Overall, the visualization reveals that most software metrics are strongly interrelated, indicating that as the size or complexity of the code increases, other metrics reflecting software effort, volume, and operations tend to rise simultaneously. This behavior highlights the intrinsic connection between code size, complexity, and maintainability.

## Specifically, the following insights can be derived:

High Positive Correlations:
Metrics such as loc (Lines of Code), v(g), ev(g), n, v, d, and e show strong positive correlations with each other and with the defects variable.
This indicates that larger and more complex code modules are more prone to defects.
In other words, as the number of lines and operations in the code increases, the likelihood of introducing errors also rises.

## Negative Correlation:
The l (Halstead Level) metric shows a negative relationship with most other variables.
This suggests that as code complexity grows, readability and simplicity (reflected by higher l values) decrease — meaning clearer and more understandable code tends to contain fewer defects.

## Weak or Neutral Correlations:
Metrics such as lOComment, lOBlank, and locCodeAndComment exhibit weak correlations with the rest.
These represent the documentation and commenting aspects of code, which vary independently of structural complexity and therefore do not strongly influence defect rates directly.

In summary, the correlation heatmap clearly demonstrates that defect occurrence in software modules is closely linked to code size and complexity.
Modules that are longer, denser, and involve more branching and operations are statistically more likely to contain bugs.
Conversely, well-structured, readable code shows a lower probability of defects.


