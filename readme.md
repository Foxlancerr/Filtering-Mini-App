<h1 style="color:yellow">Simple Filtering System Where Students View his record</h1>

    here we have 2 roles
        - admin
        -user/student

### Admin

    username: admin
    password: admin

- admin will view all the records of student,his marks,percentage,pass/fail status and also filter it.

### User

    username: user
    password: 11111, 22222, 33333, 44444, 55555


- user will view there marks and not view other user marks

<h3 style="color:yellow">Pages</h3>

- login page
- Student Data page
- Admin page

<h3 style="color:yellow">Working Procedure</h3>

There are the following function used

1. function <code>getTotalMark</code>
```js
//make to create function which calculate students marks
function getTotalMark(marksArr) {
    let total = 0;
    for (let mark of marksArr) {
        total += mark;
    }
    return total;
}
```

2. function <code>getTotalMark</code>
```js
//make to create function which calculate students marks
function getTotalMark(marksArr) {
    let total = 0;
    for (let mark of marksArr) {
        total += mark;
    }
    return total;
}
```

3. function <code>getPercentage</code>
```js
//make to create function which calculate students marks
function getPercentage(percentArr) {
    let percentage = getTotalMark(percentArr);
    return ((percentage / maxMark) * 100).toFixed(0);
}
```