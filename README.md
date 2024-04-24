# Project Objective:

"Sports Basics" is a sports blog company that entered space recently. They wanted to get more traffic to their website by releasing a special edition magazine on IPL 2024. This magazine aims to provide interesting insights and facts for fans, analysts and teams based on the last 3 years' data (2021, 2022, 2023).

## Power BI Project Report:
Click Here to view 👇🏻
“The Masterstroke: IPL 2024’s Strategic Playbook”

https://lnkd.in/g62brqed

### Primary Insights Requirements:
1. Top 10 batsmen based on past 3 years total runs scored.
2. Top 10 batsmen based on past 3 years batting average. (min 60 balls faced in each season)
3. Top 10 batsmen based on past 3 years strike rate (min 60 balls faced in each season)
4. Top 10 bowlers based on past 3 years total wickets taken.
5. Top 10 bowlers based on past 3 years bowling average. (min 60 balls bowled in each season)
6. Top 10 bowlers based on past 3 years economy rate. (min 60 balls bowled in each season)
7. Top 5 batsmen based on past 3 years boundary % (fours and sixes).
8. Top 5 bowlers based on past 3 years dot ball %.
9. Top 4 teams based on past 3 years winning %.
10. Top 2 teams with the highest number of wins achieved by chasing targets over the past 3 years.

### Secondary Insights Requirements:
1. Pick your team selecting the Best 11 players based on their positions, 3 years performance data and additional research.
2. Pick your top all-rounders.

### Challenges in IPL data:
Many players from the past are not participating in this IPL and there are many newcomers which required additional research.

### Tools used:
- Data cleaning, preprocessing - Power BI, Python (pandas)
- Data visualization - Power BI
### Steps followed:
- Extracted IPL players list from online.
- Downloaded Match summary, Batting info, Bowling info datasets from CodeBasics.
- Created a measure table to store all measures for easy accessing.
- Created new pointstable using python pandas.

            import pandas as pd
            import numpy as np
            df = pd.read_csv("C:/Users/karthik/Desktop/Raw Data/C10_Input_Files/C10_Input_Files/datasets/dim_match_summary.csv")
            df.replace({'Super Kings':'CSK', 'KKR':'KKR', 'RCB':'RCB', 'Mumbai':'MI', 'Punjab Kings':'PBKS',
                        'Sunrisers':'SRH', 'Capitals':'DC','Royals':'RR', 'Titans':'GT', 'Super Giants':'LSG'},inplace=True)


            print(df.info())
            df['matchDate'] = df['matchDate'].astype(str)
            df[['Month-Day', 'Year']] = df['matchDate'].str.split(', ', expand=True)
            print(df.info())
            df_2021 = df[['team1','team2','winner','Year']].loc[df['Year']=='2021']
            pt_2021 = pd.DataFrame()
            pt_2021['Team'] = df_2021['winner'].unique()
            pt_2021.set_index('Team',inplace=True)
            pt_2021['Matchs'] = df_2021['team1'].value_counts() + df_2021['team2'].value_counts()
            pt_2021['Won'] = df_2021['winner'].value_counts()
            pt_2021['Lost'] = pt_2021['Matchs'] - pt_2021['Won']
            pt_2021['Year'] = 2021

            df_2022 = df[['team1','team2','winner','Year']].loc[df['Year']=='2022']
            pt_2022 = pd.DataFrame()
            pt_2022['Team'] = df_2022['winner'].unique()
            pt_2022.set_index('Team',inplace=True)
            pt_2022['Matchs'] = df_2022['team1'].value_counts() + df_2022['team2'].value_counts()
            pt_2022['Won'] = df_2022['winner'].value_counts()
            pt_2022['Lost'] = pt_2022['Matchs'] - pt_2022['Won']
            pt_2022['Year'] = 2022


            df_2023 = df[['team1','team2','winner','Year']].loc[df['Year']=='2023']
            pt_2023 = pd.DataFrame()
            pt_2023['Team'] = df_2023['winner'].unique()
            pt_2023.set_index('Team',inplace=True)
            pt_2023['Matchs'] = df_2023['team1'].value_counts() + df_2023['team2'].value_counts()
            pt_2023['Won'] = df_2023['winner'].value_counts()
            pt_2023['Lost'] = pt_2023['Matchs'] - pt_2023['Won']
            pt_2023['Year'] = 2023

            new_points_table = pd.concat([pt_2021,pt_2022,pt_2023],sort=False)
            new_points_table.to_csv("C:/Users/karthik/Desktop/Raw Data/C10_Input_Files/New_Points_table.csv")
- Created calculates column for winning percentage of teams.

            Winning% = DIVIDE('New_Points_table'[Won],'New_Points_table'[Matchs])*100
- Created Team Logo and Color Tables for Logo links and Color px values.
- Performed data modelling for all Tables.
![ipl data modelling](https://github.com/karthikhariharan7/The-Masterstroke-IPL-2024-s-Strategic-Playbook-Report/assets/167401723/2c3b1d53-0343-40f7-a3c4-94922284c2a6)

- Created custom columns for Boundary runs & balls.
- Created measures for batting, bowling, team measures, top perfomers , some measures are

            Boundary% = CALCULATE(DIVIDE(sum(Fact_batting_info[Boundary Runs]),[Runs])*100)
            B_Economy = CALCULATE(DIVIDE([Runs_conceded],[Balls_Bowled]/6))
            Count_Of_Chasing_Wins = CALCULATE(COUNTROWS(Dim_match_summary),FILTER(Dim_match_summary,RIGHT(Dim_match_summary[margin],LEN("wickets")) = "wickets"))
            Strike Rate = CALCULATE(divide([Runs],[balls_faced])*100,FILTER(Dim_players_info,[balls_faced]>60))
- Used Bookmarks, Page navigation & Slicers to filter data by years.
- Used Table, Line, Scatter charts to display all data calculated.
- Hided all other pages other than main page 
- Upload the Power BI report to Power BI services.
### Key achievements:
1. Developed a Power BI report which provides insights for all requirements.
2. Report shows the best of best Batsman's, Bowlers, Allrounders and Teams in various categories.
3. Data modelling, Dax, Page navigation, Bookmarks, Slicers like various features of Power BI is used to provide an interactive report for the company.

### A quick of project:
![report main page](https://github.com/karthikhariharan7/The-Masterstroke-IPL-2024-s-Strategic-Playbook-Report/assets/167401723/b2c85b89-30ee-4d7a-b02c-9c135baaa06b)
