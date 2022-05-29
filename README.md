# Postman tests

## gr_29.postman_collection - отправление данных при помощи GET/POST
1. На адрес http://162.55.220.72:5005 послать имя и возраст методом GET: 
![image](https://user-images.githubusercontent.com/104026290/170879763-cbd68a13-a36d-4e67-95af-cb4c4775a41c.png)


2. На адрес http://162.55.220.72:5005/user_info_3 отправить имя, возраст и зарплату методом POST:
![image](https://user-images.githubusercontent.com/104026290/170879621-554514da-c0b7-43e1-92de-3c92d767d598.png)

3. На адрес http://162.55.220.72:5005/object_info_1 отправить имя, возраст, вес методом GET:
![image](https://user-images.githubusercontent.com/104026290/170879809-7d115a4b-4698-4de2-b583-558230fc49a4.png)

4. На адрес http://162.55.220.72:5005/object_info_2 отправить имя, возраст, зарплату методом GET:
![image](https://user-images.githubusercontent.com/104026290/170879836-c4de4376-01e2-4e00-9a48-d936f891ac97.png)

5. На адрес http://162.55.220.72:5005/object_info_3 отправить имя, возраст, зарплату методом GET:
![image](https://user-images.githubusercontent.com/104026290/170879877-d49344cb-fc6c-4809-a18b-75010ddd7c20.png)

6. На адрес http://162.55.220.72:5005/object_info_4 отправить имя, возраст, зарплату методом GET
![image](https://user-images.githubusercontent.com/104026290/170880086-470e19a8-9d8c-47c5-be59-ae2112cd327c.png)

7. На адрес http://162.55.220.72:5005/user_info_2 отправить имя, возраст, зарплау методом POST
![image](https://user-images.githubusercontent.com/104026290/170880172-074360cc-7882-49c5-9b6a-c2c5d317a3e5.png)

## Autotests
### 1. Задание: На адрес http://162.55.220.72:5005/first послать данные методом GET и написать автотест
Проверить, что статус код 200 и приходит строка в body
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

### 2. Задание: На адрес http://162.55.220.72:5005/user_info_3 послать данные методом POST и написать автотест
Спарсить response body в json
```js
let resp = pm.response.json();
```

Проверить, что name в ответе равно name s request (name вбить руками.)
```js
pm.test("Name is correct", function () {
    pm.expect(resp.name).to.eql("Tamirlan");
});
```

Проверить, что age в ответе равно age s request (age вбить руками.)
```js
pm.test("Age is correct", function () {
    pm.expect(resp.age).to.eql('24');
});
```

Проверить, что salary в ответе равно salary s request (salary вбить руками.)
```js
pm.test("Salary is correct", function () {
    pm.expect(resp.salary).to.eql(100000);
});
```

Спарсить request
```js
let req = request.data;
```

Проверить, что name в ответе равно name s request (name забрать из request.)
```js
pm.test("Name is correct", function () {
    pm.expect(resp.name).to.eql(req.name);
});
```

Проверить, что age в ответе равно age s request (age забрать из request.)
```js
pm.test("Age is correct", function () {
    pm.expect(resp.age).to.eql(req.age);
});
```

Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```js
pm.test("Salary is correct", function () {
    pm.expect(resp.salary).to.eql(+req.salary);
}); 
```

Вывести в консоль параметр family из response.
```js
console.log(resp.family)
```

Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```js
pm.test("Salary after 1.5", function () {
    pm.expect(resp.family.u_salary_1_5_year).to.eql(+req.salary*4);
});
```
### 3. Задание: На сервер http://162.55.220.72:5005/object_info_3 послать данные методом GET и написать автотест
// стаус код 200
 ```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

// Спарсить response body в json
```js
let resp = pm.response.json();
```

// Спарсить request
```js
let req = pm.request.url.query.toObject()
```

// Проверить, что name в ответе равно name s request (name забрать из request.)
```js
pm.test("name is correct", function () {
    pm.expect(resp.name).to.eql(req.name);
});
```

// Проверить, что age в ответе равно age из request (age забрать из request.)
```js
pm.test("age is correct", function () {
    pm.expect(resp.age).to.eql(req.age);
});
```

// Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```js
pm.test("salary is correct", function () {
    pm.expect(resp.salary).to.eql(+req.salary);
});
```

// Вывести в консоль параметр family из response.
```js
console.log(resp.family)
```

// Проверить, что у параметра dog есть параметры name.
```js
pm.test("dog exists", function () {
    pm.expect(resp.family.pets.dog).to.have.any.keys('name');
});
```

// Проверить, что у параметра dog есть параметры age.
```js
pm.test("dog has age", function () {
    pm.expect(resp.family.pets.dog).to.have.any.keys('age');
});
```

//  Проверить, что параметр name имеет значение Luky
```js
pm.test("dog is Luky", function () {
    pm.expect(resp.family.pets.dog.name).to.eql('Luky');
});
```

// Проверить, что параметр age имеет значение 4.
```js
pm.test("dog is 4 years old", function () {
    pm.expect(resp.family.pets.dog.age).to.eql(+4);
});
```

### 4. Задание: На сервер http://162.55.220.72:5005/object_info_4 послать данные методом GET и написать автотест:
// код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

// Спарсить response body в json.
```js
let resp = pm.response.json();
```

// Спарсить request.
```js
let req = pm.request.url.query.toObject()
```

// Проверить, что name в ответе равно name s request (name забрать из request.)
```js
pm.test("name is correct", function () {
    pm.expect(resp.name).to.eql(req.name);
});
```

// Проверить, что age в ответе равно age из request (age забрать из request.)
```js
pm.test("age is correct", function () {
    pm.expect(resp.age).to.eql(+req.age);
});
```

// Вывести в консоль параметр salary из request.
```js
console.log(req.salary)
```

// Вывести в консоль параметр salary из response.
```js
console.log(resp.salary)
```

// Вывести в консоль 0-й элемент параметра salary из response
```js
console.log(resp.salary[0])
```

// Вывести в консоль 0-й элемент параметра salary из response
```js
console.log(resp.salary[1])
```

// Вывести в консоль 2-й элемент параметра salary параметр salary из response.
```js
console.log(resp.salary[2])
```

 //Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
 ```js
pm.test("salaries are equal", function () {
    pm.expect(+resp.salary[0]).to.eql(+req.salary);
});
```

//  Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
```js
pm.test("salaries are equal", function () {
    pm.expect(+resp.salary[1]).to.eql(+req.salary*2);
});
```

//  Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
```js
pm.test("salaries are equal", function () {
    pm.expect(+resp.salary[2]).to.eql(+req.salary*3);
});
```


// Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
```js
for (let i=0; i < resp.salary.length; i++) {
    console.log(+resp.salary[i]);
}
```

### 5. Задание: На сервер http://162.55.220.72:5005/user_info_2 послать данные методом POST и написать автотест:
// статус 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

// спарсить response body
```js
let resp = pm.response.json();
```

// спарсить request
```js
let req = request.data;
```

// Проверить, что json response имеет параметр start_qa_salary
```js
pm.test("Start qa salary exists", function () {
    pm.expect(resp).to.have.property('start_qa_salary');
});
```

// Проверить, что json response имеет параметр qa_salary_after_6_months
```js
pm.test("Qa salary after 6 months exists", function () {
    pm.expect(resp).to.have.property('qa_salary_after_6_months');
});
```

//  Проверить, что json response имеет параметр qa_salary_after_12_months
```js
pm.test("Qa salary after 12 months exists", function () {
    pm.expect(resp).to.have.property('qa_salary_after_12_months');
});
```

// Проверить, что json response имеет параметр qa_salary_after_1.5_year
```js
pm.test("Qa salary after 1.5 year exists", function () {
    pm.expect(resp).to.have.property('qa_salary_after_1.5_year');
});
```

//  Проверить, что json response имеет параметр qa_salary_after_3.5_years
```js
pm.test("Qa salary after 3.5 years exists", function () {
    pm.expect(resp).to.have.property('qa_salary_after_3.5_years');
});
```

// Проверить, что json response имеет параметр person
```js
pm.test("person exists", function () {
    pm.expect(resp).to.have.property('person');
});
```

// Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
```js
pm.test("start qa salary are equal", function () {
    pm.expect(resp.start_qa_salary).to.eql(+req.salary);
});
```

// Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
```js
pm.test("qa salaries after 6 months are equal", function () {
    pm.expect(resp.qa_salary_after_6_months).to.eql(+req.salary*2);
});
```

//  Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
```js
pm.test("qa salaries after 12 months are equal", function () {
    pm.expect(resp.qa_salary_after_12_months).to.eql(+req.salary*2.7);
});
```

// Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
```js
pm.test("qa salaries after 1.5 year are equal", function () {
    pm.expect(resp['qa_salary_after_1.5_year']).to.eql(+req.salary*3.3);
});
```

// Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
```js
pm.test("qa salaries after 3.5 years are equal", function () {
    pm.expect(resp['qa_salary_after_3.5_years']).to.eql(+req.salary*3.8);
});
```

// Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
```js
pm.test("1 el of u_name is request salary", function () {
    pm.expect(resp.person.u_name[1]).to.eql(+req.salary);
});
```

// Проверить, что параметр u_age равен age из request (age забрать из request.)
```js
pm.test("u_age is request age", function () {
    pm.expect(resp.person.u_age).to.eql(+req.age);
});
```

// Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
```js
pm.test("qa salaries after 5 years are equal", function () {
    pm.expect(resp.person['u_salary_5_years']).to.eql(+req.salary*4.2);
});
```

// ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
```js
for (let i=0; i < resp.person.u_name.length; i++) {
    console.log(resp.person.u_name[i])
}
```

