# IPL-AUCTION-SQL
Developing auction strategy for new IPL franchise by analyzing past IPL data to create a strong
and balanced squad
DATA
You are provided with the ipl data from the first season to the 13th season which was
held in 2020. Read and analyze the data properly before loading it into your sql server.


Question -1 : 
Your first priority is to get 2-3 players with high S.R who have faced at least 500 balls. And to do that you have to make a list of 10 players you want to bid in the auction so that when you try to grab them in auction you should not pay the amount greater than you have in the purse for a particular player.
![image](https://github.com/SatendraKumar82/IPL-AUCTION-SQL/assets/174930728/0b358fc4-83b8-4dec-a2c5-3929ada3cfe9)

Code of this problem->>
WITH balls_faced AS (    SELECT batsman, COUNT(ball) AS num_balls FROM ipl_ball WHERE extras_type <> 'wides'    GROUP BY batsman), runs_scored AS (    SELECT batsman, SUM(batsman_runs) AS total_runs_scored FROM ipl_ball    GROUP BY batsman), combined_stats AS (    SELECT a.batsman, a.num_balls, b.total_runs_scored,    ROUND((b.total_runs_scored * 100.0) / a.num_balls , 2)  AS strike_rate FROM balls_faced  a  JOIN runs_scored  b ON a.batsman = b.batsman    WHERE a.num_balls > 500) SELECT * FROM combined_stats ORDER BY strike_rate DESC LIMIT 10;
![image](https://github.com/SatendraKumar82/IPL-AUCTION-SQL/assets/174930728/ea53d0e5-3595-4a1b-b1e7-85d47a0328d8)


