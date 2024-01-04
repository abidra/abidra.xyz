---
title: When you shouldn't use useState() in your code?
author: Abid Rakhmansyah
pubDatetime: 2024-01-01T10:11:06.130Z
postSlug: when-you-shouldnt-use-usestate
featured: false
draft: false
tags:
  - react.js
description: The reason why you shouldn't use useState() in your code
---

Sometimes, we habitually use `useState` to manage or store values in our code processes. However, I've noticed that `useState` takes time to save or change its state before we can utilize it. In such cases, issues may arise when implementing `useState` that, in reality, we don't actually necessarily need to use. In this article, I will explain why you should avoid using `useState()` in your code.

## Table of contents

## Introduction

`useState` is a hook inside React.js that allows functional components to manage state. The `useState` hook is used to declare state variables in functional components. It takes an initial state as an argument and returns an array with two elements: the current state value and a function that allows you to update the state.

## How do useState works?

`useState` hook returns an array with 2 elements. The function takes the initial state as an argument and returns an array containing the current state and a function to update the state. `state` is The current state value. `setState` is a function that allows you to update the state.

Below is an example of how to use `useState`:

```javascript
const [count, setCount] = useState(0);
```

`count` is the current state value while `setCount` is the function that allow you to update the state. If you call above code inside your function, it will return like this:

```javascript
console.log(count); // return 0
setCount(1); // it will change count state to 1
```

## useState is useless (sometimes)

I have observed that some people tend to overuse the `useState` hook, especially when its use is unnecessary for running certain functions. Below is an example where you can actually omit the use of `useState` in your code:

## Example 1

**Bad example ❌**:

```javascript
const [categoryName, setCategoryName] = useState("");

const handleChange = e => {
  setCategoryName(e.target.value);

  // Save name of the category to our backend
  axios
    .patch("/category", {
      category: categoryName,
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
};

return (
  <select name="category" onChange={handleChange}>
    <option value="volvo">Volvo</option>
    <option value="saab">Saab</option>
    <option value="opel">Opel</option>
    <option value="audi">Audi</option>
  </select>
);
```

In the above example, if you change the select option quickly from:

1. Volvo to Saab
2. Saab to Opel
3. Opel to Audi

The value stored in the backend can be Saab or Opel, not Audi (**the last selected option**). This is because, during the third change, the state value of **categoryName** may still be pending before it is updated.

**Good example ✅**:

```javascript
const handleChange = e => {
  const categoryName = e.target.value;

  // Save name of the category to our backend
  axios
    .patch("/category", {
      category: categoryName,
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
};

return (
  <select name="category" onChange={handleChange}>
    <option value="volvo">Volvo</option>
    <option value="saab">Saab</option>
    <option value="opel">Opel</option>
    <option value="audi">Audi</option>
  </select>
);
```

In the above example, the **categoryName** value undergoes instantaneous changes, even if you quickly switch it from:

1. Volvo to Saab
2. Saab to Opel
3. Opel to Audi.

This immediacy is achieved by not saving the value into state but instead directly using the value from `e.target.value`.

## Example 2

I have another example of when you shouldn't use useState() in your code.

**Bad example ❌**:

```javascript
const { fileId, fileName } = props;
const [fileUrl, setFileUrl] = useState("");

// Function to get pdf from API
const getFileUrl = async () => {
  const data = await fetch(`http://example.com/${fileId}/`);
  const file = new Blob([data], { type: "application/pdf" });
  const url = URL.createObjectURL(file);
  setFileUrl(url);
};

async function downloadFile() {
  await getFileUrl();
  saveAs(fileUrl, fileName); // save the file
}

return <button onClick={() => downloadFile()}>Download file</button>;
```

In the above example, there will be some delay before the state is changed in the `setFileUrl()` function. During this time, the `saveAs()` function will be executed even though the state has not changed. In this scenario, the app may fail because the `saveAs()` function will have an empty `fileUrl`. To resolve this issue, we can simply eliminate the use of `useState` and proceed with the process directly.

**Good example ✅**:

```javascript
const { fileId, fileName } = props;

async function downloadFile() {
  const data = await fetch(`http://example.com/${fileId}/`);
  const file = new Blob([data], { type: "application/pdf" });
  const url = URL.createObjectURL(file);
  saveAs(url, fileName); // save the file
}

return <button onClick={() => downloadFile()}>Download file</button>;
```

In the above example, there's no need to utilize `useState` to retrieve and store the URL value. Instead, we can directly pass the value from the current process to the next step. Consequently, the `saveAs()` function will have the correct URL value, derived directly from the preceding step.

## Conclusion

You should avoid using `useState` when the function process can proceed straightforwardly without the need to save the state. Simply utilize the inherited value from the HTML, as it doesn't incur any delay during changes. Feel free to discuss with me in the comment section. Thank you!
