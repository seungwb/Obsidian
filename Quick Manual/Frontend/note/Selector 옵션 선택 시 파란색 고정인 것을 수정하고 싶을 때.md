```html
//html
<div class="custom-dropdown">  
    <div class="selected-option deco deco-pos:right icon:RT deco-size:1 deco-color:main-6" id="selectedOptionCategory">카테고리 선택</div>  //id 설정
    <ul class="options">  
        <li class="option" data-value="1">과채</li>     //value값 설정
        <li class="option" data-value="2">앙념</li>  
        <li class="option" data-value="3">가공식품</li>  
    </ul>  
</div>
<input type="hidden" id="selectedCategory" name="categoryId" value="1"> 
					//id값설정 밑 post로 넘겨줄 원하는 변수명을 name에 설정
```
```js
//JavaScript
document.addEventListener("DOMContentLoaded", function() {  
    var selectedOption = document.getElementById('selectedOptionCategory');  
    var options = document.querySelectorAll('.option');  
    var selectedCategoryInput = document.getElementById('selectedCategory');  
  
    selectedOption.addEventListener('click', function() {  
        var optionList = this.nextElementSibling;  
        optionList.style.display = (optionList.style.display === 'block') ? 'none' : 'block';  
    });  
  
    options.forEach(function(option) {  
        option.addEventListener('click', function() {  
            var selectedValueCategory = this.getAttribute('data-value');  
            selectedOption.textContent = this.textContent;  
            selectedCategoryInput.value = selectedValueCategory; // hidden input에 선택된 값을 설정  
            this.parentNode.style.display = 'none';  
        });  
    });  
  
    // 드롭다운 닫기  
    document.addEventListener('click', function(event) {  
        if (!selectedOption.contains(event.target)) {  
            options.forEach(function(option) {  
                option.parentNode.style.display = 'none';  
            });  
        }  
    });  
});
```
```css
//css
.custom-dropdown {  
    position: relative;  
    display: inline-block;  
}  
/*처음 클릭하는 곳 스타일링*/  
.selected-option {  
    background-color: #ffffff;  
    padding: 8px 16px;  
    border: 1px solid var(--color-main-5);  
    border-radius: 5px;  
    cursor: pointer;  
    width: 250px;  
    height : 40px;  
    display: flex;  
    align-items: center;  
    justify-content: space-between;  
}  
/*메뉴 고르는곳 스타일링*/  
.options {  
    position: absolute;  
    list-style-type: none;  
    padding: 0;  
    margin: 0;  
    background-color: #ffffff;  
    border: 1px solid var(--color-main-5);  
    border-top: none;  
    border-radius: 5px;  
    display: none;  
    width: 250px;  
    align-items: center;  
    justify-content: center;  
    z-index: 1;  
}  
  
.option {  
    padding: 8px 16px;  
    cursor: pointer;  
}  
  
.option:hover {  
    background-color: var(--color-base-2); /*버튼 마우스오버 시 색상 지정*/  
}
```