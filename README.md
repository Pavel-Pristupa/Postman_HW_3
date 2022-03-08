#  # Postman_HW_3  
  
__Create requests and run tests via Postman__  

1) необходимо залогиниться  
POST  
`http://162.55.220.72:5005/login`  
login : str (кроме /)  
password : str  
  
Приходящий токен необходимо передать во все остальные запросы.

____
*дальше все запросы требуют наличие токена.*  
____

2) `http://162.55.220.72:5005/user_info`  
req. (RAW JSON)  
POST  
age: int  
salary: int  
name: str  
auth_token  
  
resp.  
```js
{
	'start_qa_salary':salary,
	'qa_salary_after_6_months': salary * 2,
	'qa_salary_after_12_months': salary * 2.9,
	'person': {
		'u_name':[user_name, salary, age],
		'u_age':age,
		'u_salary_1.5_year': salary * 4
	}
}
```  
Тесты:  
1) Статус код 200  
2) Проверка структуры json в ответе.  
3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.  
4) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса `http://162.55.220.72:5005/get_test_user`  
____
  
3) `http://162.55.220.72:5005/new_data`  
req.  
POST  
age: int  
salary: int  
name: str  
auth_token  

Resp. 
```js 
{
	'name':name,
	'age': int(age),
	'salary': [salary, str(salary*2), str(salary*3)]
}
```  
  
Тесты:  
1) Статус код 200  
2) Проверка структуры json в ответе.  
3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.  
4) проверить, что 2-й элемент массива salary больше 1-го и 0-го  
____
  
4) `http://162.55.220.72:5005/test_pet_info`  
req.  
POST  
age: int  
weight: int  
name: str  
auth_token  
  
Resp.  
```js
{
	'name': name,
	'age': age,
	'daily_food':weight * 0.012,
	'daily_sleep': weight * 2.5
}
```
  
Тесты:  
1) Статус код 200  
2) Проверка структуры json в ответе.  
3) В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент.  
____
  
5) `http://162.55.220.72:5005/get_test_user`  
req.  
POST  
age: int  
salary: int  
name: str  
auth_token  
  
Resp.
```js
{
	'name': name,
	'age':age,
	'salary': salary,
	'family':{
		'children':[['Alex', 24],['Kate', 12]],
		'u_salary_1.5_year': salary * 4
	}
}
```
  
Тесты:  
1) Статус код 200  
2) Проверка структуры json в ответе.  
3) Проверить что занчение поля name = значению переменной name из окружения  
4) Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age  
____
  
  ***Следующие пункты задания пока недоступны в связи с отсутствием ответа от сервера***
  
6) `http://162.55.220.72:5005/currency`  
req.  
POST  
auth_token  
  
Resp. Передаётся список массив объектов.  
```js
[
{
	"Cur_Abbreviation": str,
	"Cur_ID": int,
	"Cur_Name": str
},
{
	"Cur_Abbreviation": str,
	"Cur_ID": int,
	"Cur_Name": str
}
]
```
  
Тесты:  
1) Можете взять любой объект из присланного списка, используйте js random.  
В объекте возьмите Cur_ID и передать через окружение в следующий запрос.  
____
  
7) `http://162.55.220.72:5005/curr_byn`  
req.  
POST  
auth_token  
curr_code: int  
  
Resp.  
```js
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}
```
  
Тесты:  
1) Статус код 200  
2) Проверка структуры json в ответе.  
____

***  
1) получить список валют  
2) итерировать список валют  
3) в каждой итерации отправлять запрос на сервер для получения курса каждой валюты  
4) если возвращается 500 код, переходим к следующей итреации  
5) если получаем 200 код, проверяем response json на наличие поля "Cur_OfficialRate"  
6) если поле есть, пишем в консоль инфу про фалюту в виде response  
```js
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}
```
7) переходим к следующей итерации  
