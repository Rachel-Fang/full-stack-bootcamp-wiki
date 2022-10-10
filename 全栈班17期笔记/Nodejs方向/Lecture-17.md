# Lecture 17 React-4
## 1.Conditional render
### 1.1 Wrapper component
- pass content by children
- further exactraction
- improved reusability
- 如何保证map id不重复
  - 使用uuid
```js
//ExpenseItem.js
import './ExpenseItem.css';
import ExpenseDate from './expenseDate/ExpenseDate';
import ExpenseItemCard from "../expenseItemCard/ExpenseItemCard";

const ExpenseItem = (props) => {

  const content = (
    <>
      <ExpenseDate date={props.date}/>
      <div className='expense-item__description'>
        <h2 className='expense-item__title'>{props.title}</h2>
        <div className='expense-item__price'>{props.amount}</div>
      </div>
    </>
  );

    return (
      <ExpenseItemCard>
        {content}
      </ExpenseItemCard>
    );
}

export default ExpenseItem;
```
```js
//ExpenseItemCard.js
import './ExpenseItemCard.css';

// children
const ExpenseItemCard = (props) => {
  return (
    <div className='expense-item-card'>
      {props.children}
    </div>
  );
}

export default ExpenseItemCard;
```
## 2.Add a year filter 
```js
//Expenses.js
import './Expenses.css';
import ExpenseItem from "./expenseItem/ExpenseItem";
import { v4 as uuid } from 'uuid';
import ExpensesFilter from "./expensesFilter/ExpensesFilter";
import {useState} from "react";

const Expenses = (props) => {
    const [filter, setFilter] = useState('2022');

    const filteredExpenses =
      props.expenses.filter(
        expense => expense.date.getFullYear().toString() === filter
      );

    const onFilterChange = (filter) => {
        setFilter(filter);
    }

    const isFilteredResultEmpty = filteredExpenses.length === 0;

    const expenseItems = filteredExpenses.map(expense => {
        return (
          <ExpenseItem
            key={uuid()}
            title={expense.title}
            date={expense.date}
            amount={expense.amount} />
        );
    })

    return (
        <div className="expenses">
            <ExpensesFilter
              onSelectFilter={onFilterChange}
                selected={filter}
            />
            {!isFilteredResultEmpty ?
              expenseItems :
              <p className='no-expense-found-msg'>No expenses found.</p>}
        </div>
    );
}

export default Expenses;
```
```js
//ExpensesFilter.js
import './ExpensesFilter.css';

const ExpensesFilter = (props) => {
  const years = ['2022', '2021', '2020', '2019'];

  const onSelect = (event) => {
    const selected = event.target.value;
    props.onSelectFilter(selected);
  }

  return (
    <div className='expenses-filter'>
      <div className='expenses-filter__control'>
        <label>Filter by year</label>
        <select value={props.selected} onChange={onSelect}>
          {years.map(year => <option key={year}>{year}</option>)}
        </select>
      </div>
    </div>
  );
}

export default ExpensesFilter;
```
## 3.Promise 
### 3.1 异步
 - 同步代码执行流程
 ![[]](./img/lecture17-1.jpg)
 - 异步代码执行流程
 - example1
  ![[]](./img/lecture17-2.jpg) 
👇
 ![[]](./img/lecture17-3.jpg)
 - example2
   - img.src = '' 这句话执行的时候就会触发render
 ![[]](./img/lecture17-4.jpg)
 ### 3.2 Promise and life cycle
 ![[]](./img/lecture17-6.jpg)
  ![[]](./img/lecture17-7.jpg)
## 4.AJAX 允许我们用后端数据
 ![[]](./img/lecture17-5.jpg)
 ### 4.1 XMLHttpRequest
 - JSON.parse() json->js 
 - render出的卡片顺序取决于数据返回的先后
 - 镶嵌结构会出现回调地狱 - fetch来解决
 ```js
 'use strict';

const countriesContainer = document.querySelector('.countries');

function renderCountry(country) {
  const html = `
    <article class="country">
      <img class="country__img" src="${country.flag}" />
      <div class="country__data">
        <h3 class="country__name">${country.name}</h3>
        <h4 class="country__region">${country.region}</h4>
        <p class="country__row"><span>👫</span>${(country.population / 1000000).toFixed(1) + ' M'}</p>
        <p class="country__row"><span>🗣️</span>${country.languages[0].name}</p>
        <p class="country__row"><span>💰</span>${country.currencies[0].name}</p>
      </div>
    </article>
  `;

  countriesContainer.insertAdjacentHTML('beforeend', html);
  countriesContainer.style.opacity = 1;
}

function getCountry(country) {
  const request = new XMLHttpRequest();

  request.open('GET', `https://restcountries.com/v2/name/${country}`);

  request.send();

  request.addEventListener('load', function () {
    const data = JSON.parse(this.responseText);
    const country = data[0];

    if (!country.borders) {
      return;
    }

    const neighbour = country.borders[0];
    const neighbourRequest = new XMLHttpRequest();

    neighbourRequest.open('GET', `https://restcountries.com/v2/alpha/${neighbour}`);

    neighbourRequest.send();

    neighbourRequest.addEventListener('load', function () {
      const country = JSON.parse(this.responseText);
      renderCountry(country);
    })

    renderCountry(country);
  })
}

getCountry('china');
getCountry('australia');
//use fetch to get data
fetch('https://restcountries.com/v2/name/china').then(data => console.log(data.json()));
```

