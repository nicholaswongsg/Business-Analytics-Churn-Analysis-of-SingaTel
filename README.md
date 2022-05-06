# Business Analytics - Churn Analysis of SingaTel - RapidMiner
# 1. Introduction
The purpose of this report is to investigate the issue of Customers leaving SingaTel and subscribing to its competitors by identifying the common and key attributes that contributed to those who have left, likely to leave in the near future and why.

To accomplish this objective, we will be conducting a data mining analysis using a complete dataset containing attributes regarding information on customers who have left SingaTel since Jan 2017 as well as those of existing customers.

# Contributors

<table>
  <tr>
    <th>Member</th>
    <th>Contributions</th>
    <th>Github</th>
  </tr>
  <tr>
    <td>Nicholas Wong Jia Hao</td>
    <td>-</td>
    <td>@nicholaswongsg</td>
  </tr>
  <tr>
    <td>Lim Zeng Kit</td>
    <td>-</td>
    <td>@</td>
  </tr>
  <tr>
    <td>Ong Wei Zhi</td>
    <td>-</td>
    <td>@</td>
  </tr>
</table>

# 2.1 Problem Defination
There is a concern regarding customers that leave SingaTel and subscribing to its competitors. Customers are precious assets to companies, and are essential to the survival of these companies. Therefore, in order to maintain a good customer base and ensuring the success of the company, SingaTel has decided to engage the analytics team to identify attributes contributing to customers who have left and likely to leave in the future. Using the data collected, the analytics team will seek to understand the customer’s reasons for churning and propose solutions.

# 2.2 Business Objective
The business objective of SingaTel is to analyze the customers who have left and most likely to leave in the future, and their reasons for leaving. After which, recommendations will be proposed to SingaTel to help them retain their existing customers and discourage churn.

# 3.1 Import Dataset
Starting off our data analysis, we will first import the given dataset into RapidMiner using the ‘Read Excel’ operator. After which, we will connect it to a ‘Store’ operator to store the data within the new repository in its ‘Data’ folder.
<img src="img/Import Data set.png" alt="Import Dataset">

# 3.2 Retrieve Operator
After storing the data set into the SingaTel repository, our next step is to use the ‘Retrieve’ operator to retrieve the data from the repository and display it in a table.
<img src="img/Retrieve Operator p1.png" alt="Retrieve Operator">
<br>
<img src="img/Retrieve Operator p2.png" alt="Retrieve Operator">

As seen from the 2 screenshots of the table above, the retrieve operator worked as intended. However, before the data can be used for further analysis, a few issues have to be resolved. In this case, we must first trim the data, followed by removing missing data, replacing wrong data, and to format certain data to currency format.


# 4.1 Fixing Issues
After identifying the issues with the data above, we created a new process, retrieved the data from the previous process and have used the trim, filer examples, replace, and format numbers operators in order to clean the data and resolve the earlier issues.
<img src="img/Fix Issues.png" alt="Fix Issues">

<b>Trim Operator:</b>
The Trim operator creates new attributes from the selected nominal attributes by removing leading and trailing spaces from the nominal values. The required attributes can be selected through parameters.

<b>Remove Missing Data Operator:</b>
The remove missing operator helps to clean the data by removing the rows that have missing tenure and total charges data which allows it to be more accurate when performing the decision tree and performance at the later stage.

<b>Replace Wrong Data:</b>
The Replace operator changes the value of attributes which are wrong and replaces them with the right values for data analysis. For example, we replaced ‘No Internet Service’ with ‘No’ as the values should be standardized to either ‘Yes’ or ‘No’.

<b>Format To Currency Operator:</b>
As monthly and total charges show the amount customer paid, it should be 2 decimal places in currency format, instead of number format. Therefore, we used format to currency operator for the data for both monthly and total charges. 

# 4.2 Remove Attributes
Next, after the data has been cleaned and sorted, we will create a new process, retrieve the data from the previous process and then remove attributes which we feel is not a good predictor in our churn analysis using the ‘Select Attributes’ operator.
<img src="img/Remove Attributes.png" alt="Remove Attributes">

The attributes that we have chosen to remove and our reasons are:

<b>Contract:</b>
This attribute takes into account if the customer is in a contract with SingaTel. We have decided that it is not an attribute we should factor into when executing our churn analysis as it is not a deciding factor if they would stay with SingaTel or leave to their competitor.

<b>Customer ID:</b>
The customer ID is a unique set of numbers given to each customer to differentiate customers. As this number is auto-generated, it does not predict or show whether a customer leaves or stay. Therefore, it is not a good predictor for churn analysis. 

<b>Device Protection:</b>
With more advance phone cases and screen protector for the market to protect their phone, there will be less demand for device protection for cases where the user drop their phone or lost their phone. For lost phone, each device from Apple and Samsung comes with an in-build application like “Find my iPhone” or “Find Device”.

<b>Gender:</b>
A customer’s gender is determined when he/she is born. Each customer either falls under male or female. Both genders, male or female will sign up for a mobile plan or internet services to get connected. Thus, having a minimal impact on the customers’ decision to leave or stay which in turns, we have removed this attribute. 

<b>Online Security:</b>
With more security software like McAfee and Norton available on Google Play and App Store, device protection add-on from carrier has become the least of their consideration when choosing which carrier they are thinking of signing up a mobile plan.  

<b>Tech Support:</b>
Tech Support is the monitoring and maintaining of computer systems and networks. If customers face any issues, such as forgotten password, viruses or email issues, Tech Support is what they will be looking for. However, this has minimal impact on whether a customer leaves or stay as it is less important as compared to internet service or TV service. Therefore, it is removed. 

<b>Total Charges:</b>
The total charges are totally dependent on the monthly charges and the tenure, which is the months of subscription. As the tenure goes up, the total charges also go up, which means that the higher the tenure, the higher the total charges. By knowing the total charges each customer paid, it does not help in the churn analysis. Therefore, it is removed. 

# 4.3 Set Role
After removing the undesired attributes, we will then use the ‘Set Role’ operator to set the role of ‘Churn’ to ‘Label’ because Churn is the attribute that we want to predict through this data analysis. Thus, through this step we will be making the churn column as our special attribute. The result of this process is shown in the table below.

<img src="img/Set Role p1.png" alt="Set Role">
<img src="img/Set Role p2.png" alt="Set Role">

# 5.1 Split Data
The Split Data operator takes an ExampleSet as its input and delivers the partitions of that ExampleSet through its output ports. The number of partitions and the relative size of each partition is specified through the partitions parameter. We selected stratified sampling as our sampling attribute. This will build random subsets and ensures that the class distribution in the subsets is the same as in the whole.

First, we will execute the previous process, followed by a ‘Split Data’ operator using the ratio of 0.7 and 0.3. The reason is to split the data into 2 different models, one for training model and the other for testing model. Our selection of data ratio for the split is 0.7 and 0.3 as we want to use 30% of data for testing and 70% of data for training model. This will allow us to perform churn analysis to predict which customers are most likely to leave SingaTel base on the past data (training data which was 70%) it was being fed. The system is then being tested on the split data (testing data which was 30%) to test for the accuracy of the system.

<img src="img/Evaluate Model Performance.png" alt="Evaluate Model Performance">

# 5.2 Decision Tree
Next, we will add in a ‘Decision Tree’ operator into the process.

<img src="img/Decision Tree p1.png" alt="Decision Tree">
<img src="img/Decision Tree p2.png" alt="Decision Tree">
<img src="img/Decision Tree p3.png" alt="Decision Tree">
<img src="img/Decision Tree p4.png" alt="Decision Tree">
This is the result of the Decision Tree generated.

# 5.3 Testing Accuracy
Finally, we will be testing the accuracy of the model we have created by using the ‘Performance’ operator with the help of “Apply Model” from the previous decision tree process.

<img src="img/Testing Accuracy p1.png" alt="Testing Accuracy">
<img src="img/Testing Accuracy p2.png" alt="Testing Accuracy">
<img src="img/Testing Accuracy p3.png" alt="Testing Accuracy">
<img src="img/Testing Accuracy p4.png" alt="Testing Accuracy">

These are the results generated by the performance operator regarding the accuracy of the model.

# 6.1 Evaluate Model Performance
After validating the model of using the ratio of 0.7 and 0.3 for training and testing model respectively, it showed that the model was 77.38% accurate.

The precision for the prediction of non-churn was 81.21% (1,387/(1,387+321)*100%) as most of the predictions were correct and most customers did not churn. The precision for the prediction of churn was 60.71% (238/(154+238)*100%) as more than half of the predictions were correct and more than half churned.

We were able to get an accuracy of 90.01% (1,387/(1,387+154)*100%) for non-churn customers and accuracy of 42.58% (238/(321+238)*100%) for churn customers.

The Area Under Curve (AUC) (Optimistic) has a value of 0.866. 
The AUC has a value of 0.785
The AUC (Pessimistic) has a value of 0.704.

<img src="img/Evaluate Model Performance.png" alt="Evaluate Model Performance">

# 6.2 Evaluate Decision Tree Results
In our special attribute, churn column, we look at the customers if they have left. “Yes” representing the customer are predicted to leave SingaTel whereas “No” suggesting that the customers will remain loyal to SingaTel.

In our first group of customer (at least 2.5 months of being subscribed), those who aren’t subscribed to internet service are predicted to stay as loyal customers. (889 distribution with 18.89% ratio of total) Those who are subscribed to internet service are split further into the tenure which is more than 49.5 months or less than or equal to 49.5 months. More than 49.4 months tenure customers are loyal whereas less than or equal to 49.5 months are further divided into 17.5 months (mobile service) or less than or equal to 17.5 months tenure (senior citizen).

In mobile service, we can see that those who are senior citizen are likely to leave SingaTel (distribution 63 with 3.28 ratio of total) and those having a tenure of less or equal to 7.5 months are likely to leave too (138 distribution with 5.96% ratio of total).

In senior citizen, those who have less or equal to 18.5 months of tenure with TV service are likely to leave while those more than 18.5 months tenure and without TV service are likely to stay as loyal customer.

In our second group of customer (less than 2.5 months of being subscribed), those who are subscribed to internet service are likely to leave. (143 distribution with 9.49% ratio of total) Those who don't subscribe to internet service can be further split into senior citizen or adults. Senior citizen is likely to churn (1 distribution with 0.08% ratio of total) while adults are likely to be loyal.

Our group discovered critical insights which can aid the sales and marketing director of SingaTel. We have identified 5 categories of churn groups which is further analyzed below to provide recommendation to keep the predicted churn customers. 

<ul>
  <li>Senior citizen who’s having Internet service (less than or equal 14.5 months) and TV service (less than or equal 18.5 months)</li>
  <li>Senior citizen who’s having more than 2.5 tenure with internet service (less than or equal to 49.5 months) and having mobile service (less than or equal to 17.5 months)</li>
  <li>Adults who're having more than 2.5 tenure with internet service (less than or equal to 49.5 months) and having mobile service (less than or equal to 17.5 months)</li>
  <li>Senior citizen who’s having less than or equal to 2.5 months with no internet service</li>
  <li>Adults having tenure less or equal to 2.5 months with internet service</li>
</ul>

Our insight suggests that churn customers that are senior citizen are slightly more than half which is an interesting insight for us. For the senior citizen who is churn, generally they are subscribed to internet service which seems to be essential. The only variable factor is TV service and mobile service.

On the other hand, we found out that churn adults are also both subscribed to internet service. The only variable factor is mobile service which they subscribe less than or equal to 7.5 months. 

# Conclusion
After taking into consideration all the factors we have discussed above, we have come up with the following recommendation for SingaTel to dissuade their customers from churning, specifically the senior citizens and adults.

<b>Special offer for Senior Citizens:</b>
For the senior citizens, some of the recommendations include providing them with some extra channels for their TV services as senior citizens typically enjoy watching TV at home and having more channels is likely to persuade them to remain with SingaTel.
Also, to help senior citizens with their movie streaming, a free router will be included whenever they recontract their internet service early.
Lastly, an additional 1gb of data per month will be included in their contract if they renew their contract early. This persuades the senior citizens from churning through contract renewal promotions and freebies.

<b>Special offer for Adults:</b>
For the adults, they typically watch less TV and instead use more of internet services and mobile services. Therefore, to persuade adults to remain with SingaTel, we have come up with an early renewal plan which includes a free gift as well as extra 2gb of data for the first 3 months when they renew their contracts early.
Lastly, regarding internet service, we have also come up with a plan to provide the adults with a free new router whenever they renew their internet service contract, thereby persuading them to remain as customers of SingaTel by promoting contract renewal with enticing promotions and freebies.

# References
<ul>
  <li>-</li>
  <li>-</li>
</ul>
