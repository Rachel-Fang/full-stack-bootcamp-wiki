# Lecture 19 React-5
## 1.Promise
### 1.1 Definition
 ![[]](lecture19-1.jpg)
 - 买彩票的例子：
 create a promise --waiting--> 开奖 settled resolved -> 中奖 fulfilled / 没中 rejected
 ------------------async task-----------------------------------------------------
 ### 1.2 Example
 - try catch 用在 async await
```js
'use strict';

const countriesContainer = document.querySelector('.countries');

function renderError(error) {
  countriesContainer.insertAdjacentText('beforeend', error.message);
}

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
}

// function getCountry(country) {
//   const request = new XMLHttpRequest();
//
//   request.open('GET', `https://restcountries.com/v2/name/${country}`);
//
//   request.send();
//
//   request.addEventListener('load', function () {
//     const data = JSON.parse(this.responseText);
//     const country = data[0];
//
//     if (!country.borders) {
//       return;
//     }
//
//     const neighbour = country.borders[0];
//     const neighbourRequest = new XMLHttpRequest();
//
//     neighbourRequest.open('GET', `https://restcountries.com/v2/alpha/${neighbour}`);
//
//     neighbourRequest.send();
//
//     neighbourRequest.addEventListener('load', function () {
//       const country = JSON.parse(this.responseText);
//       renderCountry(country);
//     })
//
//     renderCountry(country);
//   })
// }

const getCountry = (country) => {
  const request = fetch(`https://restcountries.com/v2/name/${country}`);
  console.log(request);
  request
    .then(response => response.json())
    .then(data => {
      const country = data[0];
      renderCountry(country);
      if (!country.borders) {
        return;
      }
      const neighbour = country.borders[0];
      // 避免callback hell
      return fetch(`https://restcountries.com/v2/alpha/${neighbour}`);
    })
    .then(response => response.json())
    .then(data => renderCountry(data))
    .catch(error => renderError(error))
    .finally(() => {
      countriesContainer.style.opacity = 1;
    });
}

// manual error throwing

const getCountryBetter = async (country) => {
  try {
    const response = await fetch(`https://restcountries.com/v2/name/${country}`);
    const data = await response.json();
    const firstFoundCountry = data[0];
    renderCountry(firstFoundCountry);

    if (!firstFoundCountry.borders) {
      throw new Error('This country has no neighbour, please try a different one.');
    }
    const neighbour = firstFoundCountry.borders[0];
    const neighbourRes = await fetch(`https://restcountries.com/v2/alpha/${neighbour}`);
    const neighbourCountry = await neighbourRes.json();
    renderCountry(neighbourCountry);
  } catch(error) {
    renderError(error);
  } finally {
    countriesContainer.style.opacity = 1;
  }
}

const btn = document.querySelector('.btn-country');

btn.addEventListener('click', () => getCountryBetter('australia'));

// getCountryBetter('china');
```

## 2. Event Loop
 ![[]](lecture19-2.jpg)
 ### 2.1 Example
  ![[]](lecture19-3.jpg)
  👇
  addeventlistener 的callback被放入callback queue的时机完全取决于异步操作所需时长
  ![[]](lecture19-4.jpg)
  👇
  非promise的callback是Macro task queue
  promise的callback是micro task queue
  ![[]](lecture19-6.jpg)
  - 伪代码实现异步操作
  ![[]](lecture19-5.jpg)
  ### 2.2 优先级
  sync code > promise callback code > callback code
  - promise callback的代码不能过长，不然callback很难执行到
## 3. Async Await
- 所有的async function返回的东西都是一个promise
- await后面一定跟一个promise
- await下面行里的所有内容直到async function结尾都会包含在await promise.then()里面 （await 工作原理）
```js
// manual error throwing

const getCountryBetter = async (country) => {
  try {
    const response = await fetch(`https://restcountries.com/v2/name/${country}`);
    const data = await response.json();
    const firstFoundCountry = data[0];
    renderCountry(firstFoundCountry);

    if (!firstFoundCountry.borders) {
      throw new Error('This country has no neighbour, please try a different one.');
    }
    const neighbour = firstFoundCountry.borders[0];
    const neighbourRes = await fetch(`https://restcountries.com/v2/alpha/${neighbour}`);
    const neighbourCountry = await neighbourRes.json();
    renderCountry(neighbourCountry);
  } catch(error) {
    renderError(error);
  } finally {
    countriesContainer.style.opacity = 1;
  }
}

```