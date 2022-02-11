# ServiceTimeHeatMap_SQL_PowerQuery_PowerPivot

#Pupose
The purpose of this project was to give the requesting department an ad-hoc report that could measure their service times to each respective customer in minutes. The requirements included;
1.	The report can be refreshed with one click (Accomplished)
2.	The data separate out erroneous outliers automatically (Accomplished)
3.	The tool be easy for managers to use (Accomplished)
4.	The results be visually digestible (Accomplished)

In all, 3 meeting were held with stakeholders prior to roll out and a presentation was given along with key insights that were discovered in the process.

# Steps to Create the Tool

# Step 1

SQL Query written to draw data directly from data base


SELECT dbo.fact_TaskLifeCycle.YARD_ID, dbo.fact_TaskLifeCycle.CreatedTimeStamp, dbo.fact_TaskLifeCycle.AssignedTimeStamp, dbo.fact_TaskLifeCycle.PinnedTimeStamp, dbo.fact_TaskLifeCycle.CompletedTimeStamp, c3.dim_TaskType.Abbreviation_Lang1 AS Request_Release, c3.dim_Zone.Path_Lang1 AS Origin, dim_Zone_1.Path_Lang1 AS Destination, dbo.fact_TaskLifeCycle.Task_ID
FROM dbo.fact_TaskLifeCycle INNER JOIN c3.dim_Zone ON dbo.fact_TaskLifeCycle.OriginZONE_ID = c3.dim_Zone.Zone_ID INNER JOIN c3.dim_Zone AS dim_Zone_1 ON dbo.fact_TaskLifeCycle.DestinationZONE_ID = dim_Zone_1.Zone_ID INNER JOIN c3.dim_TaskType ON dbo.fact_TaskLifeCycle.TaskType_ID = c3.dim_TaskType.TaskType_ID
WHERE (NOT (dbo.fact_TaskLifeCycle.CompletedTimeStamp IS NULL)) AND (NOT (c3.dim_TaskType.Abbreviation_Lang1 = N'GATEIN')) AND (NOT (dbo.fact_TaskLifeCycle.CreatedTimeStamp IS NULL)) AND (dbo.fact_TaskLifeCycle.YARD_ID = 1)
AND (dbo.fact_TaskLifeCycle.PinnedTimeStamp > CONVERT(DATETIME, '2021-01-01 00:00:00', 102)) OR (dbo.fact_TaskLifeCycle.YARD_ID = 2)

# Step 2
Cleanse and format data with Power Query
 
![image](https://user-images.githubusercontent.com/44706605/153673576-fa5becad-4d54-49ed-8bc9-ad65c9706672.png)
 
 
# Step 3
Use Excel Power Pivot to create relationships between the database tables and custom tables that assign locations to owners
 
 ![image](https://user-images.githubusercontent.com/44706605/153673593-b2b0e85a-872f-4dd1-be2b-f6b9a18a596f.png)

 
# Step 4
Conduct analysis to determine outliers and other descriptive statistics  

![image](https://user-images.githubusercontent.com/44706605/153673655-256aaee5-3b69-446d-8969-468981855581.png)


# Step 5
Create presentation to Stakeholders using statistics found in step #4 to determine final direction regarding outliers and statistical methodologies used See Service Report Presentation Power Point
 
 ![image](https://user-images.githubusercontent.com/44706605/153673674-7db6a9b6-b612-46a8-9f61-ce10de92e27d.png)

 
 
# Step 6

Create pivot table according to agreed upon specifications
 

![image](https://user-images.githubusercontent.com/44706605/153673687-d54d340f-1ba2-49cd-b42d-2b49a90ed12a.png)
