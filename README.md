# 1. Retrieve the top 5 highest-rated cinema halls

``` diff
select name, rating, location 
from cinema 
order by rating desc 
limit 5;
```
<img width="790" alt="Screenshot 2025-02-26 at 12 36 52 AM" src="https://github.com/user-attachments/assets/56897ae2-028b-4b0e-bd27-a3fb7cfa9b82" />

# 2. Find the cinema hall with the most reviews

``` diff
select name, review_count 
from cinema 
order by review_count desc 
limit 1;
```
<img width="790" alt="Screenshot 2025-02-26 at 12 38 59 AM" src="https://github.com/user-attachments/assets/5c020110-5c17-4152-827e-6cf2709815a4" />

# 3. Calculate the average rating per genre

``` diff
select genre, avg(rating) as avg_rating 
from cinema 
group by genre;
```
<img width="790" alt="Screenshot 2025-02-26 at 12 40 18 AM" src="https://github.com/user-attachments/assets/1de975c4-989d-439b-8ebc-9d539b6257d7" />
