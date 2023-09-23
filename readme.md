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

1. <code>Selection of html elements</code>

```js
//selection
let filterBtn = document.getElementById("filter-btn");
let option = document.getElementById("option");
let tBody = document.getElementById("tbody");

//login form selection
let nameSpan = document.getElementById("name-h2");
let genderSpan = document.getElementById("gender-h2");
let marksSpan = document.getElementById("marks-h2");
let percentageSpan = document.getElementById("percentage-h2");
let messageBox = document.getElementById("message-box");
let loginBox = document.getElementById("login-box");
let studentBox = document.getElementById("student-data-box");
let adminBox = document.getElementById("admin-data-box");
let loginBtn = document.getElementById("login-btn");
```

<h3 style="color:yellow">Events Listeners</h3>

The following events listener is used

1. For loginBtn

```js
//addeventlistner when user/admin click on login butoon
loginBtn.addEventListener("click", function () {
  let pswd = document.getElementById("passward").value;
  let userId = document.getElementById("username").value;

  //here is find method used which check the student and admin have enter into login and see the queries
  let student = students.find(function (student) {
    return student.username === userId && student.passward === pswd;
  });
  console.log(student);
  student.role === "admin"
    ? loginAdminFunc(student)
    : loginStudentFunc(student);
});
```

2. for filteringBtn

```js
filterBtn.addEventListener("click", function () {
  let optionText = option.value;
  console.log(option.value);
  getFilterData(optionText);
});
```

<h3 style="color:yellow">All Functions</h3>

There are the following function used

1. function <code>getTotalMark()</code>

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

2. function <code>getPercentage()</code>

```js
//make to create function which calculate students percentage
function getPercentage(percentArr) {
  let percentage = getTotalMark(percentArr);
  return ((percentage / maxMark) * 100).toFixed(0);
}
```

3. function <code>hasPass()</code>

```js
//make to create function which show which students is pass/fail
function hasPass(haspassArr) {
  let stuPassFail = getPercentage(haspassArr);
  return stuPassFail >= 45 ? "pass" : "fail";
}
```

4. function <code>displaystudentRecord()</code>

```js
//make to create function which display students record
function displaystudentRecord(studentArr) {
  studentArr.forEach(function (elem) {
    let stuMarkReturn = getTotalMark(elem.marks);
    let stuPercentageReturn = getPercentage(elem.marks);
    let hasPassReturn = hasPass(elem.marks);
    // console.log(stuMarkReturn);
    // console.log(stuPercentageReturn);
    // console.log(hasPassReturn);

    let html = `
                <tr>
                    <td>${elem.name}</td>
                    <td>${elem.gender}</td>
                    <td>${stuPercentageReturn}%</td>
                    <td>${stuMarkReturn}</td>
                    <td>${hasPassReturn}</td>
                </tr>
            `;
    tBody.insertAdjacentHTML("beforeend", html);
  });
}
```

6. function <code>getFilterData()</code>

```js
//make to create function which filter students data based on the option value
function getFilterData(optionValue) {
  let stuFilterData = [];
  tBody.innerHTML = ""; //make the tbody empty when we call display students record

  switch (optionValue) {
    case "male":
      stuFilterData = students.filter((stu) => stu.gender === "male");
      break;
    case "female":
      stuFilterData = students.filter((stu) => stu.gender === "female");
      break;
    case "pass":
      stuFilterData = students.filter((stu) => hasPass(stu.marks) === "pass");
      break;
    case "fail":
      stuFilterData = students.filter((stu) => hasPass(stu.marks) === "fail");
      break;
    default:
      stuFilterData = students;
  }
  displaystudentRecord(stuFilterData); //call a students record function
}
```

7. function <code>loginAdminFunc()</code>

```js
//when admin enter we can hide loginbox,studentbox and unhide adminbox.
function loginAdminFunc() {
  loginBox.classList.add("hidden");
  adminBox.classList.remove("hidden");
}
```

8. function <code>loginStudentFunc()</code>

```js
//when admin enter we can hide loginbox,adminbox and unhide studentbox.
function loginStudentFunc(students) {
  nameSpan.textContent = students.name;
  genderSpan.textContent = students.gender;
  marksSpan.textContent = getTotalMark(students.marks);
  percentageSpan.textContent = getPercentage(students.marks) + "%";
  messageBox.innerHTML = getMessage(students);

  loginBox.classList.add("hidden");
  studentBox.classList.remove("hidden");
}
```

9. function <code>getMessage()</code>

```js
//we can send a message to a current login student whether its fail/pass in the exam
function getMessage(students) {
  let passed = hasPass(students.marks);
  let percent = getPercentage(students.marks);
  let message = "";

  if (passed === "pass") {
    message = `<p><span>Congrujulation!</span> you have ${passed} <br>
         the exam and your score is ${percent} </p>`;
    messageBox.style.background = "rgba(0, 255, 0, 0.781)";
  } else {
    message = `<p><span>We are sorry!</span> you have ${passed} <br>
         the exam and your score is ${percent}% </p>`;
    messageBox.style.background = "rgba(255, 0, 0, 0.774)";
  }
  return message;
}
```
<h2 style="color:yellow">Hide the student and admin box when the browser loaded</h2>

```js
//hide the student and admin box when the browser loaded.
studentBox.classList.add("hidden");
adminBox.classList.add("hidden");
```

<h2 style="color:yellow">Student records and Admin Records</h2>

```js
//students array
let students = [
  {
    name: "ahmad",
    username: "admin",
    passward: "admin",
    gender: "male",
    marks: [78, 67, 45, 89, 70],
    role: "admin",
  },
  {
    name: "abuzar",
    username: "user",
    passward: "11111",
    gender: "male",
    marks: [58, 77, 85, 29, 30],
    role: "user",
  },
  {
    name: "ashfaq",
    username: "user",
    passward: "22222",
    gender: "male",
    marks: [58, 67, 85, 89, 76],
    role: "user",
  },
  {
    name: "abubakar",
    username: "user",
    passward: "33333",
    gender: "male",
    marks: [98, 97, 45, 69, 30],
    role: "user",
  },
  {
    name: "kainat",
    username: "user",
    passward: "44444",
    gender: "female",
    marks: [38, 47, 45, 39, 20],
    role: "user",
  },
  {
    name: "tamanaa",
    username: "user",
    passward: "55555",
    gender: "female",
    marks: [78, 87, 75, 89, 90],
    role: "user",
  },
  {
    name: "rukai",
    username: "user",
    passward: "66666",
    gender: "female",
    marks: [58, 47, 35, 39, 40],
    role: "user",
  },
  {
    name: "zafar",
    username: "user",
    passward: "88888",
    gender: "male",
    marks: [98, 67, 75, 99, 90],
    role: "user",
  },
  {
    name: "javerya",
    username: "user",
    passward: "99999",
    gender: "female",
    marks: [98, 87, 55, 99, 90],
    role: "user",
  },
  {
    name: "ihtisham",
    username: "user",
    passward: "10101",
    gender: "male",
    marks: [28, 27, 45, 16, 50],
    role: "user",
  },
];
```
