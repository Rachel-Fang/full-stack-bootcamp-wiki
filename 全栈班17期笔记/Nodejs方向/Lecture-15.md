# Lecture 15 React-2

# 课堂笔记

## 1. 上节课作业讲解
### 1.1 ExpenseDate component

```js
// ExpenseDate.js
import './ExpenseDate.css';

function ExpenseDate(props) {
    const year = props.date.getFullYear();
    const month = props.date.toLocaleDateString('en-AU', {month: 'long'});
    const day = props.date.toLocaleDateString('en-AU', {day: '2-digit'});

    return (
        <div className='expense-date'>
            <div className='expense-date__month'>{month}</div>
            <div className='.expense-date__year'>{year}</div>
            <div className='expense-date__day'>{day}</div>
        </div>
    );
};

export default ExpenseDate;

```

```js
//ExpenseItem.js
import './ExpenseItem.css';
import ExpenseDate from './ExpenseDate';

function ExpenseItem(props) {
    return (
        <div className='expense-item'>
            <ExpenseDate date={props.date}/>
            <div className='expense-item__description'>
                <h2>{props.title}</h2>
                <div className='expense-item__price'>{props.amount}</div>
            </div>
        </div>
    );
}

export default ExpenseItem;
```
- 同时每个component本质上就是一个function所以也可以用arrow function改写。

  ```js
  // ExpenseDate.js
  import './ExpenseDate.css';

  const ExpenseDate = (props) => {
      const year = props.date.getFullYear();
      const month = props.date.toLocaleDateString('en-AU', {month: 'long'});
      const day = props.date.toLocaleDateString('en-AU', {day: '2-digit'});

      return (
          <div className='expense-date'>
              <div className='expense-date__month'>{month}</div>
              <div className='.expense-date__year'>{year}</div>
              <div className='expense-date__day'>{day}</div>
          </div>
      );
  };

  export default ExpenseDate;

  ```

  ```js
  //ExpenseItem.js
  import './ExpenseItem.css';
  import ExpenseDate from './ExpenseDate';

  const ExpenseItem = (props) => {
      return (
          <div className='expense-item'>
              <ExpenseDate date={props.date}/>
              <div className='expense-item__description'>
                  <h2>{props.title}</h2>
                  <div className='expense-item__price'>{props.amount}</div>
              </div>
          </div>
      );
  }

  export default ExpenseItem;
  ```

### 1.2 封包
  - 目的
    - 组件封包
    - 反应component tree的结构
  - component的首字母大写，但是装component的folder名字大小写都可以
  - 封包后结构：

  >components
  >> expenses
  >>> expenseItem
  >>>> expenseDate


- Q: export以及import
  - default export出的item是一个js file里export的default value，defalut import时不管修改成任何名字都是default的export出的item
  ```js
    export default Expenses;

    import MyExpenses from './components/expenses/Expenses'
  ```
  - import {item, item, ...}里的item叫做named import，是比较specific的export
  ```js
    export const name = 'Jing';
    export const age = 18;

    import {name, age} from './components/expenses/Expenses'
  ```
  - 当js file里没有明显的default export时，常常采用named export

## 2. 本节内容

### 2.1 Handle user event
  - In vanilla JS

  ```js
  // click event
  // call back
  function exampleCallBackFunction(){
      firstTitleElement.style.background = 'blue';
  }

  firstTitleElement.addEventListener('click', exampleCallBackFunction);
  ```
  - Each HTML element has a list of events it can listen to. Refer to [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API)
  - React里一个handle button click event的例子
### 2.2 Use React
- onclick里传入一个函数的ref，这样被点击的时候就知道去哪找这个函数。如果不传入函数，会在render的时候直接执行
  ```js
  //ExpenseItem.js
  import './ExpenseItem.css';
  import ExpenseDate from './ExpenseDate';

  function ExpenseItem(props) {
    
      return (
           <div className='expense-item'>
              <ExpenseDate date={props.date}/>
              <div className='expense-item__description'>
                  <h2>{props.title}</h2>
                  <div className='expense-item__price'>{props.amount}</div>
              </div>
              <button onClick={() => {console.log('I am clicked')}}>Change title</button>
          </div>
      );
  }

  export default ExpenseItem;
  ```
   - when click button, update title text to 'updated'
     - 点击button，console里title的值修改为updated，但是h2里的title没有改变
     - 想要修改title的值，就要component被重新渲染，所以如果直接修改props.title的值时不会修改显示出的title的值
  ```js
  //ExpenseItem.js
  import './ExpenseItem.css';
  import ExpenseDate from './ExpenseDate';

  function ExpenseItem(props) {
      let title = props.title;
      const onButtonClick = () => {
          title = 'updated!';
          console.log(title);
      }
    
      return (
           <div className='expense-item'>
              <ExpenseDate date={props.date}/>
              <div className='expense-item__description'>
                  <h2>{title}</h2>
                  <div className='expense-item__price'>{props.amount}</div>
              </div>
              <button onClick={onButtonClick}>Change title</button>
          </div>
      );
  }

  export default ExpenseItem;
  ```
  - 为了重新渲染component, 引入state
    - state object is where you store property values that belong to the component, when the state changes, the component re-renders
    - react update components only when state changes
    - state updates are scheduled. not resulting components update straight away. 当有几个state同时改变时，react只会一起重新渲染一次，不会渲染多次。
    - initialisation assignment happens only once
    - it's a hook (usexxx), hook的内容以后再说
  ```js
  //ExpenseItem.js
  import './ExpenseItem.css';
  import ExpenseDate from './ExpenseDate';
  import {useState} from 'react';

  function ExpenseItem(props) {
      //local state 虽然state会被render多次，但是state是相互独立的
      const [title, setTitle] = useState(props.title);

      const onChangeTitleButtonClick = () => {
          setTitle('Updated!');
      }
    
      return (
           <div className='expense-item'>
              <ExpenseDate date={props.date}/>
              <div className='expense-item__description'>
                  <h2>{title}</h2>
                  <div className='expense-item__price'>{props.amount}</div>
              </div>
              <button onClick={onChangeTitleButtonClick}>Change title</button>
          </div>
      );
  }

  export default ExpenseItem;
  ```    
  - 通过form的形式输入newExpense
  ```js
  //NewExpense.js
  import './NewExpense.css';
  import ExpenseForm from './expenseForm/ExpenseForm';
  const NewExpense = (props) => {
      return (
          <div className="new-expense">
              <ExpenseForm />
          </div>
      );
  }

  export default NewExpense;
  ```
   - 父传子 通过props
   - 子传父/爷 在父/爷里定义要调用子或者孙子的方法，把方法通过props传给拥有变量的层级
  ```js
  //App.js
  import './App.css';
  import Expenses from './Components/expenses/Expenses';
  import NewExpense from './Components/newExpense/NewExpense';
  import {useState} from 'react';

  const App = () => {
    const initalexpenses = [
      {
        date: new Date(2022, 9, 17),
        title: 'Car Insurance',
        amount: '$1500'
      },
      {
        date: new Date(2022, 9, 16),
        title: 'Toliet Paper',
        amount: '$1500'
      },
      {
        date: new Date(2022, 9, 15),
        title: 'Dinner with Friends',
        amount: '$80'
      },
      {
        date: new Date(2022, 9, 14),
        title: 'Myki',
        amount: '$50'
      },
  ]
		
	const [expenses, setExpenses]=useState(initalexpenses);
	const onAddNewExpense = (newExpense) => {	
	  setExpenses((prevState) => {	
	    return [...prevState, newExpense];	
	  });	
	  console.log('from app');	
	  console.log(newExpense);	
	}	
	return (	
	  <>
	      <NewExpense addNewExpense = {onAddNewExpense}/>
	      <Expenses expenses = {expenses}/>
	  </>
	
	);
}
export default App;
  ```
   - event.target.value 拿到event修改的值
   - event.preventDefault() 阻断所有default行为
   - 利用useState创建localstate
   - 分别给title，amount和date设置state更可读更可控
   - 如果将三个state合并在一起，setstate时也要用...prevState拷贝前一个，再修改单独一项(react提供的prevState能够保证是当下最新的state)
  ```js
  const [formData, setFormData] = useState({
   title: '',
   amount: '',
   date: ''
  });
  setFormData((prevState ) => {
    return {
      ...prevState,
      title: value
    }
  });
  ```


  ```js
  //ExpenseForm.js
  import './ExpenseForm.css';
  const ExpenseForm = (props) => {
    const [title, setTitle] = useState('');
    const [amount, setAmount] = useState('');
    const [date, setDate] = useState('');
    
    const onFormSubmit = (event) => {
      event.preventDefault();
      const formData = {title, amount, date: new Date(date)};
      props.addNewExpense(formData);
    };
    const onInputChange = (event, type) => {
      console.log(event);
      const value = event.target.value;
      console.log(value);
      switch(type) {
        case 'title':
		  setTitle(value);
		  console.log(title); 
		  break;
        case 'amount':
		  setAmount(value);
          break;
        case 'date':
          setDate(value);
          break;
        default:
          console.error('unknown type');
          break;
      } 
    };
      return (
        <form onSubmit={onFormSubmit}>
            <div className="new-expense__controls">
                <div className="new-expense__control">
                    <label>Title</label>
                    <input type="text" onChange = {(event) => onInputChange(event, 'title')}></input>
                </div>
                <div className="new-expense__control">
                    <label>Amount</label>
                    <input type="number" min="0.01" step="0.01" onChange = {(event) => onInputChange(event, 'amount')}></input>
                </div>
                <div className="new-expense__control">
                    <label>Date</label>
                    <input type="date" min='2021-09-21' max='2022-09-21' onChange = {(event) => onInputChange(event, 'date')}></input>
                </div>
            </div>
            <div className="new-expense__actions">
                <button type="submit">
                    Add Expense
                </button>
            </div>
        </form>
        
    ); 
  export default ExpenseForm;
  ```