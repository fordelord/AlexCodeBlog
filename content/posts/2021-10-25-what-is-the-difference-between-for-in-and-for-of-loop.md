---
title: What is the difference between [For In] and [For Of] loop
date: 2021-10-25 07:15:00
featuredImage: /post-images/2021-10-25-what-is-the-difference-between-for-in-and-for-of-loop.webp
draft: false
tags:
  - JavaScript
---

A week ago, I was asked this question on the interview.

And I didn't have a good answer.

So, I decided it would be 😂 hilarious to write a blog post about it.

---

Let's say we have the following object of people:

```javascript
const people = [
  {
    name: "John",
    age: 20,
  },
  {
    name: "Alex",
    age: 25,
  },
  {
    name: "Peter",
    age: 30,
  },
];
```

### For in / (Key iterator)

````

```javascript
for (person in people) {
  console.log(person);
}

// 0
// 1
// 2
````

### For of / (Value iterator)

```javascript
for (person of people) {
  console.log(person);
}

// {name: "John", age: 20}
// {name: "Alex", age: 25}
// {name: "Peter", age: 30}
```

So, basically, that's it.

Pretty simple.
