```
<insert id="save" parameterType="Order">  
    insert into `ORDER`(`DATE`, `TYPE`, PRICE, QUANTITY, DETAIL_ID, MEMBER_ID, PRODUCT_ID, LOCATION_ID)  
    VALUES(  
    current_timestamp()  
    ,#{type}  
    ,#{price}  
    ,#{quantity}  
    ,CONCAT(  
          DATE_FORMAT(current_timestamp(), '%Y%m%d')  
          ,'-', LPAD(  
                   (SELECT AUTO_INCREMENT  
                   FROM INFORMATION_SCHEMA.TABLES  
                   WHERE TABLE_NAME = 'ORDER') , 4, '0')   <!--order_id값-->  
          ,'-',LPAD(  
                   FLOOR(RAND() * 10000), 4, '0')           <!--4자리 난수-->  
          )  
    ,#{memberId}  
    ,#{productId}  
    ,#{locationId})  
</insert>
/결과 예)20240403(날짜)-0002(생성된 PK)-2342(4자리난수)
```