## Activity File: Part 2 - Defend Your SOC

- VSI recently experienced several cyberattacks, likely from their adversary JobeCorp.

- Fortunately, your SOC team had set up several monitoring solutions to help VSI quickly identify what was attacked.

- These monitoring solutions will also help VSI create mitigation strategies to protect the organization.

You have been provided two logs files of suspicious activity:
  - One for a Windows server
  - One for an Apache web server

### Windows Server Logs

Load the logs in your Splunk environment.

   - Select all default options provided.
   - **Important:** For the time range, always select **All Time**.  
    - **Important:** For the time range, always select **All Time**.  
   - **Important:** For the time range, always select **All Time**.  

Now you will review the reports you created in Part 1 and analyze the results.

#### Report Analysis for Severity

1. Access the **Reports** tab and select **Yours** to view the reports created from Part 1.

2. Select the report you created to analyze the different severities.

3. Select **Edit** > **Open in Search**.

4. Take note of the percentages of different severities.

5. Change the source from `windows_server_logs.csv` to "`source="windows_server_attack_logs.csv`

6. Select **Save**.

Review the updated results and answer the following question:

- Did you detect any suspicious changes in severity?
  - high severity went up from 7% to 20%.

#### Report Analysis for Failed Activities

1. Access the **Reports** tab and select **Yours** to view the reports created from Part 1.

2. Select the report you created to analyze the different activities.

3. Select **Edit** > **Open in Search**.

4. Take note of the failed activities percentage.

5. Change the source from `windows_server_logs.csv` to "`source="windows_server_attack_logs.csv`.

6. Select **Save**.


Review the updated results and answer the following question:

- Did you detect any suspicious changes in failed activities?
  - Failed percentage went down to 1.5% from 3% showing not much has changed there.

---
Now you will review the alerts you created in Part 1 and analyze the results.

#### Alert Analysis for Failed Windows Activity

1. Access the **Alerts** tab and select **Yours** to view the alerts created in Part 1.

2. Select the alert for suspicious volume of failed activities.

3. Select  **Open in Search**.

5. Change the source from `windows_server_logs.csv` to "`source="windows_server_attack_logs.csv`.

Review the updated results and answer the following questions:

- Did you detect a suspicious volume of failed activity?
  - yes,on Mar 25th,2020 at 3am-4am there was a spike of 70 failed activities. Previous traffic on average is around 13 per hour.

- If so, what was the count of events in the hour(s) it occurred?
  - 70

- When did it occur?
  - 03/25/20 3am-4am

- Would your alert be triggered for this activity?
  - yes

- After reviewing, would you change your threshold from what you you previously selected?
  - Threshold was set to 15 so I would increase it to prevent false positives.

#### Alert Analysis for Successful Logons

1. Access the **Alerts** tab and select **Yours** to view the alerts created in Part 1.

2. Select the alert of  suspicious volume of successful logons.

3. Select  **Open in Search**.

5. Change the source from `windows_server_logs.csv` to "`source="windows_server_attack_logs.csv`.

Review the updated results, and answer the following questions:

- Did you detect a suspicious volume of successful logons?
  - yes

- If so, what was the count of events in the hour(s) it occurred?
  - 864

- Who is the primary user logging in?
  - user j

- When did it occur?
  - 03/25/20 between 6am-8am

- Would your alert be triggered for this activity?
  - yes

- After reviewing, would you change your threshold from what you you previously selected?
  - yes, need to increase the threshold

#### Alert Analysis for Deleted Accounts

1. Access the **Alerts** tab and select **Yours** to view the alerts created in Part 1.

2. Select the alert of suspicious volume of deleted accounts.

3. Select  **Open in Search**.

4. Change the source from `windows_server_logs.csv` to "`source="windows_server_attack_logs.csv`.

Review the updated results and answer the following question:

1. Did you detect a suspicious volume of deleted accounts?  
  - no

---
 Now you will set up a dashboard and analyze the results.

#### Dashboard Setup

1. Access the **Apache Webserver Monitoring** dashboard.
    - Select **Edit**.

2. Access each panel you created and complete the following:
    - Select **Edit Search**.

    - Change the source from: `windows_server_logs.csv` to `source="windows_server_attack_logs.csv`.

    - Select **Apply**.

    - Save the dashboard.
    - Edit the time on the dashboard to be **All Time**.

#### Dashboard Analysis for Time Chart of Signatures

Analyze your new dashboard results and answer the following questions:
  - Does anything stand out as suspicious?
    - Spike in signatures over time.

  - What signatures stand out?
    - locked out user accounts, password reset attempts, small spike in user successfully logged on.

  - What time did it begin/stop for each signature?
    - Locked out accounts started after 7pm and dropped off before 10pm.
    - Password reset attempts started after 3am, peaked at 4am and dropped off before 6am.
    - Logon successful attempts started at 5am and dropped off by 7am.

  - What is the peak count of the different signatures?
    - 1792 for locked accounts
    - 2516 for password reset attempts
    - 392 for successfully logged on

#### Dashboard Analysis for Users  
Analyze your new dashboard results and answer the following questions:
  - Does anything stand out as suspicious?
    - a spike in users that's suspiciously is similar to the signatures over time chart.

  - Which users stand out?
    - user a, user k, user j

  - What time did it begin and stop for each user?
    - user a
      - start: 7am
      - stop: 10am
    - user k
      - start: 3am
      - stop: 6am
    - user j
      - start: 5am
      - stop: 8am

  - What is the peak count of the different users?
    - user a 1968
    - user k 2512
    - user j 392

#### Dashboard Analysis for Signatures with Bar, Graph, and Pie Charts
Analyze your new dashboard results and answer the following questions:
  - Does anything stand out as suspicious?
    - data is similar with users and signatures spikes.

  - Do the results match your findings in your time chart for signatures?
      - yes

#### Dashboard Analysis for Users with Bar, Graph, and Pie Charts     
Analyze your new dashboard results, and answer the following questions:
  - Does anything stand out as suspicious?
    - spikes match up with users and signatures.

  - Do the results match your findings in your time chart for users?
    - yes

#### Dashboard Analysis for Users with Statistical Charts
Analyze your new dashboard results, and answer the following question:

  - What are the advantages and disadvantages of using this report, compared to the other user panels you created?
    - advantage is I can see the data and how it relates to other data, especially over time.
    - Disadvantage would be if data in a chart has a spike but isn't related to anything malicious and I would end up up correlating data in err or spend time searching for a problem that doesn't exist.


---

### Apache Web Server Logs

Load the logs in your Splunk environment.
  - Select all default options provided.
  - **Important:** For the time range, always select **All Time**.

Now you will review the reports you created in Part 1 and analyze the results.

#### Report Analysis for Methods

1. Access the **Reports** tab and select **Yours** to view the reports created from Part 1.

2. Select the report that analyzes the different HTTP methods.

3. Select **Edit** > **Open in Search**.

4. Take note of the percent/count of the various methods.

5. Change the source from: `source=apache_logs.txt` to `source="apache_attack_logs.txt`.

6. Select **Save**.

Review the updated results and answer the following questions:

1. Did you detect any suspicious changes in HTTP methods? If so which one?
  - huge spike in POST and GET.

2. What is that method used for?
  - Sending data to a server

#### Report Analysis for Referrer Domains

1. Access the **Reports** tab and select **Yours** to view the reports created from Part 1.

2. Select the report that analyzes the different referrer domains.

3. Select **Edit** > **Open in Search**.

4. Take note of the different referrer domains.

5. Change the source from: `source=apache_logs.txt` to `source="apache_attack_logs.txt`.

6. Select **Save**.

Review the updated results, and answer the following question:
1. Did you detect any suspicious changes in referrer domains?
  - yes - http://www.semicomplete.com and http://semicomplete.com account for 86% of the referer domains.

#### Report Analysis for HTTP Response Codes

1. Access the **Reports** tab and select **Yours** to view the reports created from Part 1.

2. Select the report that analyzes the different HTTP response codes.

3. Select **Edit** > **Open in Search**.

4. Take a note of the different HTTP response codes.
5. Change the source from: `source=apache_logs.txt` to `source="apache_attack_logs.txt`.

6. Select **Save**.

Review the updated results and answer the following question:

1. Did you detect any suspicious changes in HTTP response codes?
  - 200 response codes dropped 8% and 404 went up 6%

---

Now you will review the alerts you created in Part 1 and analyze the results.
#### Alert Analysis for International Activity

1. Access the **Alerts** tab and select **Yours** to view the alerts created in Part 1.

2. Select the alert of suspicious volume of international activity.

3. Select  **Open in Search**.

4. Change the source from: `source=apache_logs.txt` to `source="apache_attack_logs.txt`.

Review the updated results and answer the following questions:

- Did you detect a suspicious volume of international activity?
  - spike from clientip country Ukraine

- If so, what was the count of the hour it occurred in?
  - 2738

- Would your alert be triggered for this activity?
  - yes

- After reviewing, would you change the threshold you previously selected?
  - yes, my threshold is too low at 140 and needs to increase.

 #### Alert Analysis for HTTP POST Activity

1. Access the **Alerts** tab and select **Yours** to view the alerts created in Part 1.

2. Select the alert of suspicious volume of HTTP POST activity.

3. Select  **Open in Search**.

4. Change the source from: `source=apache_logs.txt` to `source="apache_attack_logs.txt`.

Review the updated results, and answer the following questions:

- Did you detect any suspicious volume of HTTP POST activity?
  - yes

- If so, what was the count of the hour it occurred in?
  - 2592

- When did it occur?
  - 03/25/20 3pm-4pm

- After reviewing, would you change the threshold that you previously selected?  
  - nope

---
 Now you will set up a dashboard and analyze the results.


#### Dashboard Setup

- Access the dashboard for Apache Webserver Monitoring.

- Select **Edit**.

- Access each panel and complete the following:

    - Select **Edit Search**.

    - Change the source from: `source=apache_logs.txt` to `source="apache_attack_logs.txt`

    - Select **Apply**.

- Save the whole dashboard.

- Edit the time on the whole dashboard to be **All Time**.

#### Dashboard Analysis for Time Chart of HTTP Methods

Analyze your new dashboard results and answer the following questions:
- Does anything stand out as suspicious?
  - POST requests are higher than all other HTTP requests

- Which method seems to be used in the attack?
  - POST

- At what times did the attack start and stop?
  - started at 2pm ended at 4pm

- What is the peak count of the top method during the attack?
  - 2592

#### Dashboard Analysis for Cluster Map
Analyze your new cluster map results and answer the following questions:

- Does anything stand out as suspicious?
  - Large cluster coming from Ukraine

- Which new city, country on the map has a high volume of activity?
  - **Hint:** Zoom in on the map.
    - Kiev, Ukraine
- What is the count of that city?
  - 1744

#### Dashboard Analysis for URI Data
Analyze your dashboard panel of the URI data and answer the following questions:
- Does anything stand out as suspicious?
  - 40% of the pie is /VSI_Accounnt_logon.php

- What URI is hit the most?
  - /VSI_Accounnt_logon.php

- Based on the URI being accessed, what could the attacker potentially be doing?
  - get access to sensitive data from the company. steal secrets for JobeCorp.

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
