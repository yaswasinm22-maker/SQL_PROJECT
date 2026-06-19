Data Analyst Job Market Analysis
Introduction
This project dives into the data job market, focusing on data analyst roles. It explores top-paying jobs, in-demand skills, and identifies which skills offer the best balance between high demand and high salary.

Background
This analysis is based on a comprehensive dataset of 2023 job postings. The project seeks to answer the following questions:

What are the top-paying data analyst jobs?
What skills are required for these top-paying roles?
Which skills are most in-demand for data analysts?
Which skills are the highest paying?
What are the most optimal skills to learn (high demand + high pay)?
Tools Used
SQL: For querying and data manipulation.
PostgreSQL: The database management system.
VS Code: Used as the primary IDE for writing and executing queries.
Git/GitHub: Version control and project documentation.
Analysis & Queries
(For each query, include the following format:)




1. Question: What are the top-paying data analyst jobs?
- Identify the top 10 highest-paying Data Analyst roles that are available remotely.
- Focuses on job postings with specified salaries (remove nulls).
Why? Highlight the top-paying opportunities for Data Analysts, offering insights into employment opportunities

#Query:
  SELECT
      job_id,
      job_title,
      job_location,
      job_schedule_type,
      salary_year_avg,
      job_posted_date,
      name AS company_name
  FROM
      job_postings_fact
  LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
  WHERE
      job_title_short = 'Data Analyst' AND
      job_location = 'Anywhere' AND
      salary_year_avg IS NOT NULL
  ORDER BY
      salary_year_avg DESC
  LIMIT 10

Finding:
"job_id","job_title","job_location","job_schedule_type","salary_year_avg","job_posted_date","company_name"
226942,"Data Analyst","Anywhere","Full-time","650000.0","2023-02-20 15:13:33","Mantys"
547382,"Director of Analytics","Anywhere","Full-time","336500.0","2023-08-23 12:04:42","Meta"
552322,"Associate Director- Data Insights","Anywhere","Full-time","255829.5","2023-06-18 16:03:12","AT&T"
99305,"Data Analyst, Marketing","Anywhere","Full-time","232423.0","2023-12-05 20:00:40","Pinterest Job Advertisements"
1021647,"Data Analyst (Hybrid/Remote)","Anywhere","Full-time","217000.0","2023-01-17 00:17:23","Uclahealthcareers"
168310,"Principal Data Analyst (Remote)","Anywhere","Full-time","205000.0","2023-08-09 11:00:01","SmartAsset"
731368,"Director, Data Analyst - HYBRID","Anywhere","Full-time","189309.0","2023-12-07 15:00:13","Inclusively"
310660,"Principal Data Analyst, AV Performance Analysis","Anywhere","Full-time","189000.0","2023-01-05 00:00:25","Motional"
1749593,"Principal Data Analyst","Anywhere","Full-time","186000.0","2023-07-11 16:00:05","SmartAsset"
387860,"ERM Data Analyst","Anywhere","Full-time","184000.0","2023-06-09 08:01:04","Get It Recruit - Information Technology"


Conclusion:
The remote data analytics market shows non-existent caps for compensation, scaling well beyond standard parameters. While standard titles average market equilibrium, specialized leadership roles (e.g., Meta, AT&T) or platform niches like Enterprise Risk Management (ERM) command executive pricing tiers.

⚠️ Data Anomaly Note: The position at Mantys listing $650,000 stands out as a clear outlier. In professional database audits, this points to localized variance, such as data platform scraping errors or a salary metric factoring in performance-related equity units.




2. Question: What skills are required for the top-paying data analyst jobs?
- Use the top 10 highest-paying Data Analyst jobs from first query
- Add the specific skills required for these roles
- Why? It provides a detailed look at which high-paying jobs demand certain skills,
helping job seekers understand which skills to develop that align with top salaries

#Query:
  WITH top_paying_jobs AS (
  SELECT
      job_id,
      job_title,
      salary_year_avg,
      name AS company_name
  FROM
      job_postings_fact
  LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
  WHERE
      job_title_short = 'Data Analyst' AND
      job_location = 'Anywhere' AND
      salary_year_avg IS NOT NULL
  ORDER BY
      salary_year_avg DESC
  LIMIT 10
  )
  
  SELECT
      top_paying_jobs.*,
      skills
  FROM top_paying_jobs
  INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
  INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
  ORDER BY
      salary_year_avg DESC


FIndings:
"job_id","job_title","salary_year_avg","company_name","skills"
552322,"Associate Director- Data Insights","255829.5","AT&T","sql"
552322,"Associate Director- Data Insights","255829.5","AT&T","python"
552322,"Associate Director- Data Insights","255829.5","AT&T","r"
552322,"Associate Director- Data Insights","255829.5","AT&T","azure"
552322,"Associate Director- Data Insights","255829.5","AT&T","databricks"
552322,"Associate Director- Data Insights","255829.5","AT&T","aws"
552322,"Associate Director- Data Insights","255829.5","AT&T","pandas"
552322,"Associate Director- Data Insights","255829.5","AT&T","pyspark"
552322,"Associate Director- Data Insights","255829.5","AT&T","jupyter"
552322,"Associate Director- Data Insights","255829.5","AT&T","excel"
552322,"Associate Director- Data Insights","255829.5","AT&T","tableau"
552322,"Associate Director- Data Insights","255829.5","AT&T","power bi"
552322,"Associate Director- Data Insights","255829.5","AT&T","powerpoint"
99305,"Data Analyst, Marketing","232423.0","Pinterest Job Advertisements","sql"
99305,"Data Analyst, Marketing","232423.0","Pinterest Job Advertisements","python"
99305,"Data Analyst, Marketing","232423.0","Pinterest Job Advertisements","r"
99305,"Data Analyst, Marketing","232423.0","Pinterest Job Advertisements","hadoop"
99305,"Data Analyst, Marketing","232423.0","Pinterest Job Advertisements","tableau"
1021647,"Data Analyst (Hybrid/Remote)","217000.0","Uclahealthcareers","sql"
1021647,"Data Analyst (Hybrid/Remote)","217000.0","Uclahealthcareers","crystal"
1021647,"Data Analyst (Hybrid/Remote)","217000.0","Uclahealthcareers","oracle"
1021647,"Data Analyst (Hybrid/Remote)","217000.0","Uclahealthcareers","tableau"
1021647,"Data Analyst (Hybrid/Remote)","217000.0","Uclahealthcareers","flow"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","sql"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","python"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","go"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","snowflake"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","pandas"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","numpy"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","excel"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","tableau"
168310,"Principal Data Analyst (Remote)","205000.0","SmartAsset","gitlab"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","sql"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","python"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","azure"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","aws"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","oracle"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","snowflake"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","tableau"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","power bi"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","sap"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","jenkins"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","bitbucket"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","atlassian"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","jira"
731368,"Director, Data Analyst - HYBRID","189309.0","Inclusively","confluence"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","sql"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","python"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","r"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","git"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","bitbucket"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","atlassian"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","jira"
310660,"Principal Data Analyst, AV Performance Analysis","189000.0","Motional","confluence"
1749593,"Principal Data Analyst","186000.0","SmartAsset","sql"
1749593,"Principal Data Analyst","186000.0","SmartAsset","python"
1749593,"Principal Data Analyst","186000.0","SmartAsset","go"
1749593,"Principal Data Analyst","186000.0","SmartAsset","snowflake"
1749593,"Principal Data Analyst","186000.0","SmartAsset","pandas"
1749593,"Principal Data Analyst","186000.0","SmartAsset","numpy"
1749593,"Principal Data Analyst","186000.0","SmartAsset","excel"
1749593,"Principal Data Analyst","186000.0","SmartAsset","tableau"
1749593,"Principal Data Analyst","186000.0","SmartAsset","gitlab"
387860,"ERM Data Analyst","184000.0","Get It Recruit - Information Technology","sql"
387860,"ERM Data Analyst","184000.0","Get It Recruit - Information Technology","python"
387860,"ERM Data Analyst","184000.0","Get It Recruit - Information Technology","r"



Conclusion:
To land premium-tier roles, having a single core skill is not enough; employers expect a comprehensive technical stack. Across nearly all high-paying nodes, SQL and Python are non-negotiable requirements. High-paying tiers distinguish themselves by requiring experience with cloud infrastructures (aws, azure, snowflake), big data pipelines (pyspark, databricks), and agile collaboration toolsets (git, jira).





3. Question: What are the most in-demand skills for data analysts?
- Join job postings to inner join table similar to query 2
- Identify the top 5 in-demand skills for a data analyst.
- Focus on all job postings.
- Why? Retrieves the top 5 skills with the highest demand in the job market,
providing insights into the most valuable skills for job seekers.

#Query:

  SELECT
      skills,
      COUNT(skills_job_dim.job_id) AS demand_count
  FROM job_postings_fact
  INNER JOIN skills_job_dim ON job_postings_fact. job_id = skills_job_dim. job_id
  INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
  WHERE
      job_title_short='Data Analyst'
  GROUP BY
      skills
  ORDER BY
      demand_count DESC
  LIMIT 5

Finding:
"skills","demand_count"
"sql","92628"
"excel","67031"
"python","57326"
"tableau","46554"
"power bi","39468"

Conclusion:
The global baseline for data analytics centers heavily around a distinct set of five tools. SQL is the most critical core skill, appearing in over 92,000 job listings. Traditional tracking spreadsheets (excel) continue to maintain a strong presence alongside programming tools (python), while business intelligence reporting tools are split evenly between tableau and power bi.





4. Question: What are the top skills based on salary?
- Look at the average salary associated with each skill for Data Analyst positions
- Focuses on roles with specified salaries, regardless of location
- Why? It reveals how different skills impact salary levels for Data Analysts and
helps identify the most financially rewarding skills to acquire or improve


#Query:
  SELECT
      skills,
      ROUND(AVG(salary_year_avg),0) AS avg_salary
  FROM job_postings_fact
  INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
  INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
  WHERE
      job_title_short = 'Data Analyst'
      AND salary_year_avg IS NOT NULL
      --AND job_work_from_home = True
  GROUP BY
      skills
  ORDER BY
      avg_salary DESC
  LIMIT 25

Finding:
"skills","avg_salary"
"svn","400000"
"solidity","179000"
"couchbase","160515"
"datarobot","155486"
"golang","155000"
"mxnet","149000"
"dplyr","147633"
"vmware","147500"
"terraform","146734"
"twilio","138500"
"gitlab","134126"
"kafka","129999"
"puppet","129820"
"keras","127013"
"pytorch","125226"
"perl","124686"
"ansible","124370"
"hugging face","123950"
"tensorflow","120647"
"cassandra","118407"
"notion","118092"
"atlassian","117966"
"bitbucket","116712"
"airflow","116387"
"scala","115480"


Conclusion:
The skills that command the highest financial premiums are typically specialized, low-volume technologies. Aside from localized outliers like Subversion (svn), the data shows that Web3/Blockchain development (solidity), Data Engineering/Infrastructure Automation (golang, terraform, airflow), and Advanced Machine Learning frameworks (pytorch, tensorflow, keras) fetch the highest compensation tiers in modern data operations.


5. Question: What are the most optimal skills to learn (aka it's in high demand and a high-paying skill)?
- Identify skills in high demand and associated with high average salaries for Data Analyst roles
- Concentrates on remote positions with specified salaries
- Why? Targets skills that offer job security (high demand) and financial benefits (high salaries),
offering strategic insights for career development in data analysis


#Query:
  WITH skills_demand AS (
  SELECT
      skills_dim.skill_id,
      skills_dim.skills,
      COUNT(skills_job_dim.job_id) AS demand_count
  FROM job_postings_fact
  INNER JOIN skills_job_dim ON job_postings_fact. job_id = skills_job_dim. job_id
  INNER JOIN skills_dim ON skills_job_dim. skill_id = skills_dim.skill_id
  WHERE
      job_title_short = 'Data Analyst'
      --AND job_work_from_home = True
  GROUP BY
      skills_dim.skill_id
  ),
  average_salary AS (
  SELECT
      skills_job_dim.skill_id,
      ROUND(AVG(salary_year_avg), 0) AS avg_salary
  FROM job_postings_fact
  INNER JOIN skills_job_dim ON job_postings_fact. job_id = skills_job_dim. job_id
  INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
  WHERE
      job_title_short = 'Data Analyst'
      AND salary_year_avg IS NOT NULL
      --AND job_work_from_home = True
  GROUP BY
      skills_job_dim.skill_id
  )
  
  SELECT
      skills_demand.skill_id,
      skills_demand.skills,
      demand_count,
      avg_salary
  
  
  FROM
      skills_demand
  INNER JOIN average_salary ON skills_demand.skill_id = average_salary.skill_id
  ORDER BY
      demand_count DESC,
      avg_salary DESC
  LIMIT 25


Finding:
"skill_id","skills","demand_count","avg_salary"
0,"sql","92628","96435"
181,"excel","67031","86419"
1,"python","57326","101512"
182,"tableau","46554","97978"
183,"power bi","39468","92324"
5,"r","30075","98708"
186,"sas","14034","93707"
7,"sas","14034","93707"
196,"powerpoint","13848","88316"
188,"word","13591","82941"
189,"sap","11297","92446"
74,"azure","10942","105400"
79,"oracle","10410","100964"
76,"aws","9063","106440"
61,"sql server","8304","96191"
8,"go","7928","97267"
215,"flow","7289","98020"
22,"vba","6870","93845"
185,"looker","6271","103855"
80,"snowflake","6194","111578"
187,"qlik","5693","100933"
4,"java","5251","100214"
92,"spark","5041","113002"
233,"jira","4753","107931"
199,"spss","4711","85293"


Conclusion:
The skills that command the highest financial premiums are typically specialized, low-volume technologies. Aside from localized outliers like Subversion (svn), the data shows that Web3/Blockchain development (solidity), Data Engineering/Infrastructure Automation (golang, terraform, airflow), and Advanced Machine Learning frameworks (pytorch, tensorflow, keras) fetch the highest compensation tiers in modern data operations.





Final Project Conclusion
📈 Global Insights & Takeaways
  
  The Foundation is Uniform: Regardless of location or corporate size, SQL, Excel, and Python form the baseline foundation for modern data analysis. Attempting to enter the market without a strong handle on database queries (sql) and data manipulation (excel/python) is counterproductive.
  
  Infrastructure Skills Drive Compensation Tiers: The data clearly proves that pure business intelligence reporting has a lower earning ceiling than technical data analysis. True financial leverage belongs to analysts who understand the broader data ecosystem—specifically cloud storage infrastructure (snowflake, aws, azure) and automated pipeline data movement (spark, airflow).
  
  Strategic Career Application: For a professional aiming to balance career stability with high earning potential, the ideal roadmap is to build strong core skills in SQL and Python, and then transition toward specialized cloud architecture fields like Snowflake and advanced cloud analytics tools. This approach helps avoid the lower pay scales of generic administrative work while ensuring you remain competitive for top-tier remote roles.
