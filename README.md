# SQL-for-Recommended-programs
This SQL code was used by me to find the 30 most utilized programs in a particular industry 

select top 30 a.item_desc_long as Program_Title, count (distinct a.order_line_sk) as total_registrations
from vw_order_and_return_detail a
left join vw_item_interest_area b
 on a.item_key = b.item_key
left join vw_item_detail c
 on a.item_key = c.item_key
left join orders d
on a.order_line_sk = d.order_line_sk
where a.Usage_date between '2022-07-26' and '2023-08-30'
and d.date_cancel is null and a.order_rma = 'order' and d.order_status_key = '3' and a.org_name != 'practising law institute'
and a.item_class_Desc in ('live webcast','on-demand web programs','live webcast briefing','on-demand web briefing')
and a.parent_org_pk in (“,”,”)
--and b.interest_area_desc_long like '%X%' --replace X with IA tag
group by a.item_desc_long
order by total_registrations desc
;
