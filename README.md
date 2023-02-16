![Postman](https://alternative.me/media/256/postman-icon-zztu05pn6jviqfbd-c.png)


# Postman

Have hands-on experience in API-testing using Postman:
- created tests, collections and run them
- set up the environments
- used snippets as is and edited them to particular needs
- wrote my own autotests
- etc

```JSON        
{
    "age": "66",
    "family": {
        "children": [
            [
                "Beavis",
                14
            ],
            [
                "Butthead",
                15
            ]
        ],
        "pets": {
            "cat": {
                "age": 3,
                "name": "Murzik"
            },
            "dog": {
                "age": 4,
                "name": "Sharik"
            }
        },
        "family_salary": 1000
    },
    "name": "Ozzy",
    "salary": 666
}
```
___
Here some autotests code:

```java script
let req_f = pm.request.url.query.toObject() 
let resp_f = pm.response.json();
let req_name = req_f.name
let resp_name = resp_f.name
let req_age = +req_f.age
let resp_age = resp_f.age
let resp_salary_2 = +resp_f.salary[1]
let resp_salary_3 = +resp_f.salary[2]

pm.test("Check name", function () {
    pm.expect(req_name).to.eql(resp_name);
});
pm.test("Check age", function () {
    pm.expect(req_age).to.eql(resp_age);
});
console.log(req_f.salary)
console.log(resp_f.salary)
console.log(resp_f.salary[0])
console.log(resp_f.salary[1])
console.log(resp_f.salary[2])

pm.test("Check salary-1", function () {
    pm.expect(+req_f.salary).to.eql(resp_f.salary[0]);
});

pm.test("Check salary-2", function () {
    pm.expect(+req_f.salary*2).to.eql(resp_salary_2);
});
pm.test("Check salary-3", function () {
    pm.expect(+req_f.salary*3).to.eql(resp_salary_3);
});

pm.environment.set('name', resp_f.name);
pm.environment.set('age', resp_f.age);
pm.environment.set('salary', req_f.salary);

for (i=0; i<resp_f.salary.length; i++) {
console.log(resp_f.salary[i])}
```
