# Assessing Loan Approval Using Machine Learning

## 1. Introduction
The primary aim of this Machine Learning project is to assess the likelihood of loan approval or denial for small businesses. Our preliminary work involves selecting an appropriate dataset from the US Small Business Administration (SBA). Since its inception in 1953, the SBA has been instrumental in aiding entrepreneurs in gaining access to the US credit markets, either partially or wholly supported by US financing mechanisms.

Analyzing data related to this domain could yield significant insights into the criteria banks utilize for the approval of SBA loans. This investigation not only sheds light on the mechanisms behind financial support for small businesses but also contributes to understanding the impact of such financial decisions on social benefits and employment growth. This perspective is crucial for delineating the broader economic implications of loan approval processes, hence offering a foundation for more informed policy-making and financial practices tailored to foster small business development.

### 1.1 Business Context
Access to credit is a crucial factor for the success of small businesses within the dynamic sector. The loan approval process, influenced by complex algorithms and financial policies, presents significant challenges for many small enterprises due to the opaque criteria. This project aims to demystify these loan approval mechanisms by analysing data from the SBA, shedding light on their economic implications.

### 1.2 Problem Statement
The importance of small businesses to economic growth and employment is well-recognized, yet the loan approval criteria set by banks, under SBA's guidance, remain unclear. This opacity is a big obstacle for small businesses in obtaining necessary funding. By employing machine learning techniques to evaluate SBA loan data, this project seeks to determine factors influencing loan approval decisions.

### 1.3 Objectives
This report explores the use of machine learning to analyze SBA loan data, with the goal of uncovering the criteria banks use for loan decisions. The analysis aims to provide insights into the financial support mechanisms for small businesses, offering a deeper understanding of their economic and social implications, including effects on employment growth.

## 2. Data Origin and Preliminary Assessment

The dataset of this study originates from the US Small Business Administration, an entity with a storied history of supporting entrepreneurial endeavours. The data comprises an expansive 899,164 records, each capturing a distinct loan application across 27 data fields. Initial analysis revealed that the dataset contained a wealth of information pertinent to the loan application process. Data fields encompassed a range of factors, from the financial details of the loan sought to the demographic characteristics of the applicant businesses. Include unique identifiers and categorical variables such as 'LoanNr_ChkDgt', 'Name', 'City', 'State', 'Zip', 'Bank', and 'Bank State' pose challenges, including computational demands and high unique counts. 'City' and 'Zip' are particularly noted for their vast unique values, making them impractical for categorical use. Although 'State' and 'Bank State' have fewer unique values and might offer modelling potential, their immediate utility is limited. 'NAICS' codes, representing industry classifications.

## 3. Data Cleaning and Exploratory Data Analysis (EDA)
The exploratory data analysis commenced by checking the formats of the variables and converting them into the appropriate ones. The analysis also highlighted the distribution of these values, revealing the predominance of two specific values within the dataset and accounting for the presence of NaN values, thereby providing a comprehensive overview of the data's composition.

Further steps in the analysis included the transformation of the 'ApprovalDate' column from a string format, denoting dates as 'dd-month-yy', into a pandas DateTime object. This adjustment facilitated more accurate temporal analyses. Additionally, the 'ApprovalFY' column, which represents the fiscal year of approval, was converted from a string to an integer to enable numerical operations and comparisons.

Monetary values represented in columns such as 'DisbursementGross', 'GrAppv', and 'SBA_Appv' underwent cleansing to remove formatting characters and were converted from strings to floats. This standardization was critical for conducting financial analyses and comparisons. Rows with missing or unparseable 'ApprovalDate' entries were removed, including a few entries that ended with an 'A' without a clear explanation, rendering them unusable and highlighting the importance of data cleanliness.

The cleaning process also extended to the 'DisbursementDate', with rows missing this information being excluded from the dataset. This step underscored the importance of having complete loan disbursement records for thorough analysis. Moreover, the dataset was filtered to retain only rows with non-missing 'MIS_Status', which indicates the loan's outcome (e.g., Paid In Full or Charged Off), ensuring clarity on the loan's end status.

Feature engineering played a pivotal role in the preprocessing stage. Columns with excessive unique categorical values, such as 'City' and 'Zip', were examined for potential impact and complexity reduction techniques. Meanwhile, 'NAICS' codes, despite their numeric nature, were treated as categorical due to their finite and discrete nature.

Lastly, the analysis involved recoding various columns to better represent the categorical nature of the data. For example, 'NewExist' was cleaned to include only meaningful categories (existing or new businesses), and 'FranchiseCode' was simplified to a binary indicator of franchise affiliation, streamlining the dataset for more focused and effective analyses.

## 4. Data Quality Assessment
The highest positive correlation present is between ApprovalFY (approval fiscal year) and UrbanRural_Urban (businesses located in urban areas), which suggests that there may have been an increase in the approval of loans for urban businesses over the years. This could be reflective of the growth and development of urban areas, as well as a shift in economic policy or focus on urban centers which tend to have higher business density, infrastructure, and potentially better resources for business growth.

Conversely, there is a notable negative correlation between ApprovalFY and PercentageBySBA (the percentage of the loan guaranteed by the SBA), indicating that over the years, the SBA may be guaranteeing a smaller percentage of each loan. This might suggest a shift towards risk mitigation strategies by the SBA, or an indication of changing policies regarding their level of involvement in loan guarantees. This could also reflect a strengthening economy where businesses are deemed more creditworthy, requiring less SBA backing, or an increased confidence in the financial institutions' ability to bear more risk.

Other correlations that stand out, though less strongly, include the positive relationship between GrAppv (gross amount approved) and NewExist (whether a business is new or existing). New businesses may often require larger loans to cover startup costs, which could explain this relationship. The positive correlation between RetainedJob (number of jobs retained) and MIS_Status could suggest that loans are more likely to be paid in full when they contribute to retaining employment, potentially due to the business’s ongoing operations and sustained income.

It is crucial to remember that correlation does not imply causation. These correlations do not necessarily indicate that one variable causes the other to occur; they simply indicate that there is a relationship that could warrant further investigation. In the context of loan approvals and business success, many external factors and variables not captured in this dataset have a considerable influence, making it hard to fully understand correlations, fortunately, none are too high to affect the modelling.

In summary, while the data does not reveal any strong direct correlations with MIS_Status, the relationships observed reflect realistic trends in business financing and economic policy over the years. Further exploration, with more data and a wider business understanding, would be necessary to uncover more subtle patterns and relationships within these variables.

## 5. Models
In pursuit of the project's objective to predict loan approval outcomes, two advanced machine learning models were employed: Gradient Boosting Machines (GBM) and Random Forest Classifiers. These models were chosen for their robustness in handling large and complex datasets, as well as their ability to capture non-linear patterns that might elude simpler models, and their ability to handle imbalanced datasets. 

### 5.1 Random Forest
The Random Forest model evaluated for predicting loan outcomes demonstrates notable proficiency, as evidenced by its performance metrics and analysis of the confusion matrix. Specifically, the model exhibits a precision of 0.85 for predicting loan rejections, meaning 85% of loans it identifies as rejected are indeed correctly classified. Its recall rate for rejections stands at 0.81, capturing 81% of actual rejections, and the F1-score of 0.83 indicates a well-balanced precision-recall trade-off for this classification. Conversely, the model's precision for loan approvals is impressively higher at 0.95, ensuring that 95% of predicted approvals are accurate. The recall for approvals is even higher at 0.96, enabling the model to correctly identify 96% of all actual approvals, with an F1-score of 0.95, highlighting a good balance between precision and recall for approved loans.

Overall, the model achieves macro and weighted averages across precision, recall, and F1-score at 0.90, 0.89, and 0.89, and 0.93, respectively, underscoring its strong performance across both classifications. The confusion matrix further reinforces this, with a substantial number of true positives (95,174) and true negatives (21,880), indicating robust identification of loan approvals and rejections. However, the presence of false positives (5,148) and false negatives (3,894) suggests areas for enhancement, particularly in minimizing incorrect loan decisions.
Recommendations for improving the model include addressing the observed class imbalance through resampling techniques like SMOTE, refining the decision threshold to mitigate the trade-off between false positives and false negatives, conducting feature importance analysis for better prediction insights, further tuning the model with cross-validation to prevent overfitting, and detection methods for outlier management.

### 5.2 Gradient Boosting Machines
The Gradient Boosting Machines (GBM) model exhibits precision for predicting loan rejections (Class '0') of 0.87, which means it accurately identifies rejections 87% of the time, outperforming Random Forest's precision for the same category. Its recall rate for rejections is 0.85, indicating that it successfully identifies 85% of all true rejections, showcasing an improvement over Random Forest's recall. The F1-score for rejections is 0.86, pointing to a superior balance between precision and recall compared to Random Forest.
For loan approvals (Class '1'), GBM achieves a precision of 0.96, mirroring its high reliability in correctly predicting approvals, a figure that aligns closely with Random Forest's precision for approvals. The recall for approvals also hits 0.96, demonstrating GBM's effectiveness in identifying the correct approvals. The F1-score for this class is 0.96, reflecting an exemplary precision-recall balance for approved loans.
Overall, GBM slightly surpasses Random Forest in accuracy, precision, recall, and F1-scores, particularly excelling in the accurate classification of loan rejections. The improvement in precision and recall for both approval and rejection classes underline GBM's enhanced capability in accurately classifying loans. This performance edge suggests GBM's iterative correction and leveraging of decision trees strengthens its predictive accuracy, especially in discerning loan rejections with greater precision.

## 6. Results
### 6.1 Main Findings

Upon the application of these models to the SBA dataset, several key findings emerged:
-	Overall, the GBM model slightly outperforms the Random Forest, suggesting that this model should be the one adopted by the startup to more accurately assess whether to grant a loan with higher reliability.
-	Precision and recall metrics for both models indicated a strong predictive capacity, with the GBM model demonstrating a slight edge in identifying loan rejections.
-	The F1-score, which balances precision and recall, was favorable for both models across the classification tasks, confirming their efficacy in the prediction of loan approval outcomes.
  
### 6.2 Confusion Matrix Analysis

Analysis of the confusion matrices revealed that both models performed well in identifying true positives (approved loans) and true negatives (rejected loans). The number of false positives (loans incorrectly approved) and false negatives (loans incorrectly rejected) were low for both models, although the GBM model showed a better precision-recall trade-off, particularly in the context of loan rejections. Moreover, it is important to note that, given the imbalance of the dataset, accuracy is not the appropriate measure to look at, since it might lead to false insights due to the different dimensions of the two classes.

### 6.3 Comparative Assessment
 
The GBM model demonstrated an incremental improvement over the Random Forest in accuracy and class-specific metrics, particularly for loan rejections. The GBM’s refined approach to correcting misclassifications through successive iterations gave it a slight advantage in predictive performance. In conclusion, both classifiers show robust performance, but their suitability depends on the particular emphasis of the loan approval process whether it is to avoid risk (GBM) or to capture as many potential approvals as possible (Random Forest). By providing a clearer understanding of the factors influencing loan approval decisions, this models   contributes to predicting SBA loans, by understanding the criteria banks use for loan decisions. 

Lastly, the data-driven insights provided by these models can inform policy development and program enhancement within the SBA. Understanding the patterns and predictors of loan success and failure enables the SBA to tailor its programs to better meet the needs of small businesses, fostering an environment where small businesses can thrive.

