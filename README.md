# Airbnb-Listings-SQL-Analysis
Bu repository-də Airbnb listings dataseti üzərində MySQL istifadə edərək etdiyim analiz tapşırıqları yerləşir.
[SQL task  (Tərlan N.) 20260424.sql](https://github.com/user-attachments/files/27061892/SQL.task.T.rlan.N.20260424.sql)
-- 1. Hər bir "neighbourhood_group_cleansed" və "room_type" üçün "price" sütununun cəmini tapın.
<details>
  <summary>Həlli gör</summary>
```select neighbourhood_group_cleansed,room_type,sum(price) as sum_price
from airbnb_listings
group by 1,2;```
  
-- 2. Hər bir "property_type" və "room_type" üçün unikal "neighbourhood" dəyərlərinin sayını tapın.
select property_type,room_type,count(distinct neighbourhood) as count_neighbourhood
from airbnb_listings
group by 1,2;
-- 3. Hər bir "neighbourhood" və "room_type" üçün "price" sütununun orta qiymətini tapın.
select neighbourhood,room_type,round(avg(price),1) as avg_price
from airbnb_listings 
group by 1,2;
-- 4. Hər bir "neighbourhood_group_cleansed" və "property_type" üçün "minimum_nights" sütununun maksimum və minimum dəyərlərini tapın.
select neighbourhood_group_cleansed,property_type,min(minimum_nights) as min_nights,max(minimum_nights) as max_nights
from airbnb_listings
group by 1,2;
-- 5. Hər bir "host_location" və "host_is_superhost" üçün elanların sayını tapın.
select host_location,host_is_superhost,count(*) as listing_count
from airbnb_listings
group by 1,2;
-- 6. Hər bir "neighbourhood_cleansed" və "property_type" üçün elanların sayını və "price" sütununun ortalamasını tapın.
select neighbourhood_cleansed,property_type,count(*) as listing_count,round(avg(price),1) as avg_price
from airbnb_listings
group by 1,2;
-- 7. Hər bir "room_type" və "neighbourhood_group_cleansed" üçün "price" sütununun maksimum dəyərini tapın.
select room_type,neighbourhood_group_cleansed,max(price) as max_price
from airbnb_listings
group by 1,2;
-- 8. "minimum_nights" dəyəri 2-dən az olan və "room_type" "Private room" olan elanların sayını "property_type"-a görə tapın.
select property_type,count(*) as count_listings
from airbnb_listings
where minimum_nights < 2
and room_type ='Private room'
group by 1
order by count_listings DESC;
-- 9. "host_name" və "host_location" sütunlarını birləşdirərək elanların sayını tapın.
select concat(host_name,'-',host_location) as host_info,count(*) as count_listings
from airbnb_listings
group by 1;
-- 10. "price" sütunu 100-dən çox olan və "neighbourhood_cleansed" "Eixample" olan elanların orta qiymətini "neighbourhood_cleansed", "room_type" görə tapın.
select neighbourhood_cleansed,room_type,round(avg(price),1) as avg_price
from airbnb_listings
where price > 100
and  neighbourhood_cleansed like '%Eixample%'
group by 1,2;
-- 11. Hər bir "host_response_time" və "host_response_rate" üçün ev sahiblərinin ("host_name") sayını tapın.
select host_response_time,host_response_rate,count(distinct host_name) as 'count of host_name'
from airbnb_listings
group by 1,2;
-- 12. "host_name" sütununun ilk 3 hərfi və "host_id" ilə elanların sayını tapın.
select substr(host_name,1,3) as '3 of host_name', host_id,count(*) as count_listings
from airbnb_listings
group by 1,2;
-- 13. "host_acceptance_rate" 90%-dən yuxarı olan elanların sayını "room_type"+"host_identity_verfied", "Entire home/apt" görə hesablayın.
SELECT concat(room_type,' - ',host_identity_verified),COUNT(*) AS count_listings
FROM airbnb_listings
WHERE host_acceptance_rate > '90%'
AND room_type = 'Entire home/apt'
GROUP BY room_type,host_identity_verified;
-- 14. Hər bir "neighbourhood" və "property_type" üçün "price" sütununun maksimum və minimum dəyərlərini tapın.
select neighbourhood,property_type,max(price) as max_price,min(price) as min_price
from airbnb_listings
group by 1,2;
-- 15. "host_name" ilk 2 hərfi "An" ilə başlayan, "room_type" və "host_acceptance_rate" üçün elanların sayını tapın.
select room_type,host_acceptance_rate,count(*) as listings_count
from airbnb_listings
where host_name like 'An%'
group by 1,2;
-- 16. "neighbourhood_group_cleansed" və "room_type" üçün elanların sayını tapın, nəticəni 10 qeydlə məhdudlaşdırın.
select neighbourhood_group_cleansed,room_type,count(*) as count_listings
from airbnb_listings 
group by 1,2
order by count_listings DESC
limit 10;
-- 17. Hər bir "neighbourhood" və "room_type" üçün elanların sayını tapın və "listings_count" > 5 olan qrupları göstərən şərtlə nəticələri məhdudlaşdırın.
select neighbourhood,room_type,count(*) as count_listings
from airbnb_listings
group by 1,2
having count_listings >5;
-- 18. "host_location" "Barcelona" ilə başlayan, hər bir "neighbourhood_cleansed" və "host_acceptance_rate" üçün elanların sayını tapın.
select neighbourhood_cleansed,host_acceptance_rate,count(*) as count_listings
from airbnb_listings 
where host_location like 'Barcelona%'
group by 1,2;
-- 19. Hər bir "property_type" və "room_type" üçün "price" sütununun ortalamasını tapın və nəticəni 5 qeydlə məhdudlaşdırın.
select property_type,room_type,round(avg(price),1) as avg_price
from airbnb_listings
group by 1,2
order by avg_price DESC 
limit 5;
-- 20. Hər bir "host_has_profile_pic" və "host_identity_verified" üçün elanların sayını tapın.
select host_has_profile_pic,host_identity_verified,count(*) as count_listings
from airbnb_listings 
group by 1,2;
