# SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk


## Overview:
This project focus on monitoring and analyzing Web Traffic Logs in Splunk

## Objective:
1. Monitor web traffic in real-time
2. Detect suspicious IP activity
3. Identify brute-force and anomaly patterns
4. Visualize security insights using dashboards

## Tool Used:
1. Splunk
2. file : "apache_logs.json"

## Dashboard Features:
1. Total Web Requests.
2. Successful Responses.
3. client Error.
4. Client Error.
5. Top Requested URLs.
6. Top users by IP Address.
7. Web Traffice by Client IP Address.


## steps :
1. *Total Web Requests*<br>
   **Query**: source="apache_logs.json" host="webserver" sourcetype="_json" | stats count AS "Total Web Requests"<br>
   **Explanation**: Select Data from apache web serve log file which contain all HTTP requests<br>
   

![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/42d3954098ed1d47f0f4c440cc91a7cd3efa3047/Screenshot%20(155).png)


2. *Successful Responses*<br>
   **Query**: source="apache_logs.json" host="webserver" sourcetype="_json" method="GET" status 200 | stats count AS "Successful Responses"<br>
   **Explanation**: Filters only GET requests .These are requests where users fetch data (web pages, images, etc.) status=200<br>
    Filters only responses with HTTP status code 200<br>
    Means: Request was successful<br>
    count all request and rename them as "Successful Responses"<br>

    
![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/60bde24de5fb7585fd44978509351048cfbb239a/Screenshot%20(122).png)


3.*Client Error(4xx)*<br>
  **Query**: source="apache_logs.json" host="webserver" sourcetype="_json" | where status>=400 and status<500 |stats count AS "Client Errors(4xx)"<br>
  **Explanation**: where status>=400 AND status<500 <br>
    Filters only HTTP status codes between 400–499<br>
    These are called Client Errors (4xx)<br>
    Counts all filtered events and Renames output column to Client Errors (4xx)<br>




4.*client Error(5xx)*<br>
   **Query**:source="apache_logs.json" host="webserver" sourcetype="_json" | where status>500 |stats count AS "Client Errors(5xx)"<br>
   **Explanation**: Filters HTTP status codes greater than 500<br>
     These are Server Errors (5xx):<br>
                       500 → Internal Server Error<br>
                       502 → Bad Gateway<br>
                       503 → Service Unavailable<br>
                      504 → Gateway Timeout<br>


5.*Top Requested URLs*<br>
   **Query**: source="apache_logs.json" host="webserver" sourcetype="_json"| stats count AS "Hits" by uri<br>
   **Explanation**: count → counts number of requests<br>
     by uri → groups data by each URL/path<br>
     AS "Hits" → renames count column to Hits<br>
     This query groups web requests by URI and counts how many times each page was accessed.<br>


6.*Top Users by IP Address*<br>
   **Query**: source="apache_logs.json" host="webserver" sourcetype="_json" |stats count AS IP by ip<br>
   **Explanation**: count → counts number of requests<br>
    by ip → groups data by each IP address<br>
    AS IP → renames the count column to IP<br>


7.*Web Traffic By Client IP Address*
   **Query**: source="apache_logs.json" host="webserver" sourcetype="_json" method="GET" |table ip | iplocation ip | stats count by Country | geom geo_countries featureIdField="Country"<br>
   **Explanation**: Table ip-  Keeps only the IP address field<br>
   | iplocation ip - Converts IP addresses into geographic data<br>
                      Adds fields like: Country, City, Latitude / Longitude<br>
   | stats count by Country - Groups data by Country<br>
                              Counts how many requests came from each country<br>
   | geom geo_countries featureIdField="Country" - Converts data into a world map visualization<br> 
                                                   Matches country names with map boundaries<br>
![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/27003cb4f0b1454ce0461b1d7c5c8d650b020121/Screenshot%20(125).png)
![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/a4299fabf2c1da3937e31cb7093332ad0b23d426/Screenshot%20(126).png)
![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/0e8774a69b02d89978f584f3d6108b2be7f792ad/Screenshot%20(127).png)
![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/b09e816492710ee261ef8900b9debab4088a0d63/Screenshot%20(129).png)
![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/d65c70ff76864f6ff9c542c23eeab7827f0d238a/Screenshot%20(159).png)
![image alt](https://github.com/Yashita05420/SIEM-Based-Web-Traffic-Analysis-Security-Monitoring-using-Splunk-.-/blob/e94b1a4e0629abb2cabed4820aa7ee3e184eec43/Screenshot%20(154).png)
