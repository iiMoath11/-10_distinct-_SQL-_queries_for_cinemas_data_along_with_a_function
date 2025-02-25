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

# 4. count the number of cinemas per location

``` diff
select location, count(*) as cinema_count 
from cinema 
group by location 
order by cinema_count desc;
```
<img width="790" alt="Screenshot 2025-02-26 at 12 42 23 AM" src="https://github.com/user-attachments/assets/68e3ba44-51db-4cc0-939d-9c9ac022b3e5" />

# 5. retrieve all cinemas with ratings below 3

``` diff
select name, rating, location 
from cinema 
where rating < 3;
```
<img width="790" alt="Screenshot 2025-02-26 at 12 43 00 AM" src="https://github.com/user-attachments/assets/22c11d4d-c041-4ddc-9a77-e1c7c4a567c9" />

# 6. identify cinemas with missing best comments

``` diff
select name, location 
from cinema 
where best_comment is null;
```
<img width="790" alt="Screenshot 2025-02-26 at 12 44 29 AM" src="https://github.com/user-attachments/assets/90429202-1ec9-4a56-ab24-00008ea34e21" />

# 7. find the highest-rated cinema in each location

``` diff
select name, location, rating 
from cinema c1 
where rating = (select max(rating) from cinema c2 where c1.location = c2.location);
```
<img width="790" alt="Screenshot 2025-02-26 at 12 45 13 AM" src="https://github.com/user-attachments/assets/fefa7778-3fc7-4158-9ee6-382a18090afb" />

# 8. get cinemas with review counts above the average

``` diff
select name, review_count 
from cinema 
where review_count > (select avg(review_count) from cinema);
```
<img width="790" alt="Screenshot 2025-02-26 at 12 46 31 AM" src="https://github.com/user-attachments/assets/dcd9e0b0-0a0e-4bea-ba10-b326da3395b7" />

# 9. retrieve the most common cinema genre

``` diff
select genre, count(*) as genre_count 
from cinema 
group by genre 
order by genre_count desc 
limit 1;
```
<img width="790" alt="Screenshot 2025-02-26 at 12 47 25 AM" src="https://github.com/user-attachments/assets/461732f2-2648-4438-b356-35924d34e774" />

# 10. find cinemas where the best comment mentions 'screen'

``` diff
select name, best_comment 
from cinema 
where best_comment like '%screen%';
```
<img width="790" alt="Screenshot 2025-02-26 at 12 48 30 AM" src="https://github.com/user-attachments/assets/c62a810d-aae4-4251-b544-2152415f51ed" />

# bonus: function to check if a rating is valid

``` diff
delimiter //

create function check_valid_rating(rating decimal(2,1)) 
returns varchar(50) 
deterministic 
begin 
    declare result varchar(50);
    
    if rating > 5 then 
        set result = 'invalid rating: rating cannot exceed 5'; 
    elseif rating < 0 then 
        set result = 'invalid rating: rating cannot be negative'; 
    else 
        set result = 'valid rating'; 
    end if; 
    
    return result;
end //

delimiter ;

SELECT check_valid_rating(4.5);
```
<img width="790" alt="Screenshot 2025-02-26 at 12 54 22 AM" src="https://github.com/user-attachments/assets/4610db4b-e9d1-42dd-b7ef-73ade5a986e8" />

