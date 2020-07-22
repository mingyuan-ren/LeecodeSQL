https://leetcode.com/problems/rank-scores/

Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks.

+----+-------+
| Id | Score |
+----+-------+
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |
+----+-------+
For example, given the above Scores table, your query should generate the following report (order by highest score):

+-------+---------+
| score | Rank    |
+-------+---------+
| 4.00  | 1       |
| 4.00  | 1       |
| 3.85  | 2       |
| 3.65  | 3       |
| 3.65  | 3       |
| 3.50  | 4       |
+-------+---------+
Important Note: For MySQL solutions, to escape reserved words used as column names, you can use an apostrophe before and after the keyword. For example `Rank`.


solutions:

1 time spent less

# Write your MySQL query statement below
select s4.Score, s3.Rank
from 
(
    select s2.Score, row_number() over (order by s2.Score DESC) AS 'Rank'
    from
    (select distinct (s1.Score) from Scores s1) s2
) s3
join Scores s4 on s4.Score = s3.Score
Order by s3.Rank


2 directly use function dense_rank

select Scores.score, dense_rank() over (order by Scores.score DESC) AS 'Rank'
from Scores
