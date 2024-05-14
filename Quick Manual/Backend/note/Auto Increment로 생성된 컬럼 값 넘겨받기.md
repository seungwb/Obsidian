```
//mapper
<insert id="save" parameterType="Product" 
useGeneratedKeys="true" keyProperty="id">  //추가한 부분, id값을 Serviceimp로 보내줌  
    INSERT INTO PRODUCT(  
       name, price, quantity, weight, thumbnail_name, thumbnail_path,   
       exp, `desc`, state, category_id, storage_type_id, admin_id,   
       quantity_category_id, weight_category_id)   
    VALUES(  
       #{name}, #{price}, #{quantity}, #{weight}, #{thumbnailName}, #{thumbnailPath},  
       #{exp}, #{desc}, #{state}, #{categoryId}, #{storageTypeId}, #{adminId},  
       #{quantityCategoryId}, #{weightCategoryId} )  
  </insert>
```

useGeneratedKeys="true" keyProperty="넘겨 받을 컬럼명" Serviceimp로 감