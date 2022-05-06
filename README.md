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
