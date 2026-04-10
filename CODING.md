**1. Group Transactions by Category (map + reduce)**

Question

You have:

const transactions = [
  { id: 1, category: "Food", amount: 200 },
  { id: 2, category: "Travel", amount: 500 },
  { id: 3, category: "Food", amount: 300 }
];

Output:

{
  Food: 500,
  Travel: 500
}

**Solution**

const result = transactions.reduce((acc, curr) => {
  acc[curr.category] = (acc[curr.category] || 0) + curr.amount;
  return acc;
}, {});

**2. Remove duplicates from array:**

[1, 2, 2, 3, 4, 4]

Solution

const unique = arr.filter((item, index) => arr.indexOf(item) === index);

const unique = [...new Set(arr)];

**3. Flatten Nested Array (reduce)**

Question

const arr = [[1, 2], [3, 4], [5]];

Output:

[1, 2, 3, 4, 5]

Solution

const flat = arr.reduce((acc, curr) => acc.concat(curr), []);

**4. Count Occurrences of Elements**

Question

["apple", "banana", "apple", "orange", "banana"]

Output:

{
  apple: 2,
  banana: 2,
  orange: 1
}

Solution

const count = arr.reduce((acc, item) => {
  acc[item] = (acc[item] || 0) + 1;
  return acc;
}, {});

**5. Filter + Map Combined (Important)**

Question

Get names of users above age 18

const users = [
  { name: "Sai", age: 20 },
  { name: "Ram", age: 15 },
  { name: "John", age: 25 }
];

Solution

const result = users
  .filter(user => user.age > 18)
  .map(user => user.name);

**6. Find Maximum Value Using Reduce**

Question

[10, 5, 20, 8]

Solution

const max = arr.reduce((acc, curr) => Math.max(acc, curr), -Infinity);

**7. Transform Object Array to Lookup Map**

Question

const users = [
  { id: 1, name: "Sai" },
  { id: 2, name: "Ram" }
];

Output:

{
  1: { id: 1, name: "Sai" },
  2: { id: 2, name: "Ram" }
}

Solution

const map = users.reduce((acc, user) => {
  acc[user.id] = user;
  return acc;
}, {});

**8. Remove Falsy Values (filter)**

Question

[0, 1, false, 2, "", 3, null]

Solution

const clean = arr.filter(Boolean);

**9. Sum of Nested Object Values**

Question

const data = [
  { items: [{ price: 10 }, { price: 20 }] },
  { items: [{ price: 30 }] }
];

Solution

const total = data.reduce((acc, curr) => {
  return acc + curr.items.reduce((sum, item) => sum + item.price, 0);
}, 0);

**10. Chain Everything (Real Interview Level)**

Question

From orders:

const orders = [
  { status: "completed", amount: 100 },
  { status: "pending", amount: 200 },
  { status: "completed", amount: 300 }
];

Solution

const total = orders
  .filter(order => order.status === "completed")
  .map(order => order.amount)
  .reduce((sum, amt) => sum + amt, 0);
