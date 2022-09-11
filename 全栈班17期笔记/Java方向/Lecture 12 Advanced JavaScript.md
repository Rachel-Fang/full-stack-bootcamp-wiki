### 1.0 作业讲解
#### 1.1 作业详解
   首先记住三个单词：<font color=red> `Readable, Maintainable, Reusable`</font>（RMR）
  -  可读性，可维护性，可复用性（好的代码是有RMR特性的）
 作业A版本：
 ```js
function calculateTax(income)
{
    var tax = 0;
    if (0 <= income && income <= 18200) {
    
    }

    else if (18201 <= income && income <= 37000){
        tax = (income - 18200) * 19 / 100;
    }

    else if (37001 <= income && income <= 90000) {
        tax = 3572 + (income - 37000) * 32.5 / 100;    
    }

    else if (90001 <= income && income <= 180000) {
        tax = 20797 + (income - 90000) * 37 / 100;
    }

    else if (180001 <= income) {
        tax = 54096 + (income - 180000) * 45 / 100;
    }

    return tax;
}
```
- 作业B版本：
    ```js
    let salaryRange = [0, 18200, 45000, 120000, 180000],
		taxRate = [0, 0.19, 0.325, 0.37, 0.45],
		startNum = [0, 0, 5092, 29467, 51667];
		    
	function findRange(salary) {
	
	  for (let i = salaryRange.length; i >= 0; i--) {
	
	    if (salary > salaryRange[i]) {
	
	      const tax = (
	
	        (salary - salaryRange[i]) * taxRate[i] +
	
	        startNum[i]
	
	      ).toFixed(2);
	
	      return tax;
	    }
	  }
	}
    ``` 
    - 版本C：
    ```js
       
    ```
    - 上面这份代码为什么好，因为<font color=red> `符合人类正常思维`</font>，首先我们想它是不是在special case里，如果是，返回什么；如果不是在special case里，将直接返回什么
    > 为什么第三遍代码更优雅呢，因为它更符合人类正常思维 
    - 如果想写的更好，那就要<font color=red> `更符合语言的设计思路`</font>
      - 首先我们可以短路一下
      ```js
          function getStops(flights){
          const stop = flights.length() - 1;

          const specialCases = {
            0: 'Direct',
            1: '1 stop',
            7: '',
            11: 'The Dreamline',
            12: '',
            27: 'Around The World`,
          };

          const specialCase = speciaCases[stop]; 

          return specialCase || stop + 'stops';
        }
      ``` 
      - 我们为什么要声明一个变量，是因为我们希望把它保存起来以后再用，但明显这里specialCase与specialCases用不到，使用替换法，进一步精简代码，第四遍
      ```js
          function getStops(flights){
            const stop = flights.length() - 1;

            return {
              0: 'Direct',
              1: '1 stop',
              7: '',
              11: 'The Dreamline',
              12: '',
              27: 'Around The World`,
            }[stop] || stop + 'stops';
          }
      ``` 
      - 是要可读性还是要更高级
        - 如果写的是一种耳熟能详的语法，就没有牺牲它的可读性
        - 要把握住可读性与高级间的平衡点，不能为了高级而高级
      - 这种代码，你也可以写出来，首先要放弃一个观点：这个东西很简单，这样写这样写就可以（思而不学则怠）；也不能说我写出来了，能工作了，就够了（学而不思则罔）
        - 简单说就是，<font color=red> `要能够自我否定，好的代码写三遍`</font>
        > 自我否定就是：我写完了，但我就是写的不好，我尝试要写好它，我怎么才能写好它，我要绞尽脑汁的想怎么才能写好它，这个过程就是fishing的过程，要专注于过程。
#### 1.2 Readable，Maintainable，Reusable对作业优化
  - 对作业的优化：
    - 按照思维，我们要有一个taxTable, 然后通过我们注入的收入，查表，找到该收入所在的行来进行计算
    ```js
	const taxTable = [
	
	    { min: 0,       max: 18200,                     tax: 0,     rate: 0    },
	
	    { min: 18200,   max: 37000,                     tax: 0,     rate: 0.19 },
	
	    { min: 37000,   max: 90000,                     tax: 3572,  rate: 0.325},
	
	    { min: 90000,   max: 120000,                    tax: 20797, rate: 0.37 },
	
	    { min: 180000,  max: Number.POSITIVE_INFINITY,  tax: 54097, rate: 0.45 }
	
	 ];
	
	function calculateTax (income, taxTable) {
	
	    for(var i = 0; i < taxTable.length; i ++) {
	
	        if (income > taxTable[i].min && income <= taxTable[i].max) {
	
	        var tax = taxTable[i].tax + (income - taxTable[i].min) * rate;
	
	        return tax;
	        }
	    }
	}
    ```
    - 还可以更进一步按照人类正常思维优化，将符合历代澳洲40个税表的要求改完，也就是reusable：
    ```js
	function calculateTax2 (income, taxTable) {
	
	    var taxRow = taxTable.find((row) => income > row.min && income <= row.max)
	
	    var tax = taxRow.tax + (income - taxTable.min) * taxRaw.rate;
	    
	    return tax;
	    }
    ```

### 2.0 SOLID 原则 （版本秘籍走天下，只学SOD）
### 好的东西写三遍
#### 2.1 Single Responsibility: 单一职责
  -  认为对象/功能/一段代码应该仅具有一种单一功能
  -  例如课堂练习，
  ```js
    
  ```
  因此，职责分离可以修改为
  `[stop] || stop + 'stops'`  
#### 2.2 Open/Close: 开闭原则
  -  一段代码应该对当前职责的更改打开，对于其他更改关闭

#### 2.3 Liskov Subsititution: 里式替换
  -  甭看
  
#### 2.4 Iterface Segregation: 接口隔离
  -  甭看
  
#### 2.5 Dependency Inversion: 依赖反转/注入
  -  依赖注入，如果一段代码依赖于零一段代码的定义，那么定义应该独立于代码，并且注入进来。
  -  依赖一定是独立存在的事情



