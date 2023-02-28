# dateFormat , 날짜 증가/감소 공통처리 (전역변수 사용X, 함수내의 지역변수로 처리)

### [githubpage](https://soonya27.github.io/dateFormat-updateDate/)


## dateFormat
### example
```javascript
const toDayMonth = new Date();

formatDateOption(toDayMonth, 1, 'year');
formatDateOption(toDayMonth, 1, 'month');
formatDateOption(toDayMonth, 1, 'day');

formatDateOption(toDayMonth, 2, 'year');
formatDateOption(toDayMonth, 2, 'month');
formatDateOption(toDayMonth, 2, 'day');

formatDateOption(toDayMonth, 3, 'year');
formatDateOption(toDayMonth, 3, 'month');
formatDateOption(toDayMonth, 3, 'day');
```

### code
```javascript

/**
 * formatDate 타입과 범위 지정
 * @author pyeon
 * example)))
    formatDateOption(new Date(), 3, 'month')
 * @param {string} date 
 * @param {string & number} type  '-' , '.', '년월일'  Or 1,2,3
 * @param {string} range:optional   'year' , 'month' , 'day'
 * @returns string ex) '2022' , '2022.01' , '2022년 01월'
 */
function formatDateOption(date, type, range) {
    const d = new Date(date);
    let day = '' + (d.getDate()),
        month = '' + (d.getMonth() + 1),
        year = d.getFullYear();

    if (day.length < 2) day = '0' + day;
    if (month.length < 2) month = '0' + month;

    const types = [
        { numId: 1, keyword: '-', text: ['-', '-'] },
        { numId: 2, keyword: '.', text: ['.', '.'] },
        { numId: 3, keyword: '년월일', text: ['년', '월', '일'] },
    ];
    const selectedType = types.find((item) => type == item.numId || type == item.keyword);

    let returnDate = '';
    switch (range) {
        case 'year':
            if (selectedType.numId == 3) {
                returnDate = year + selectedType.text[0];
            } else {
                returnDate = year;
            }
            break;
        case 'month':
            if (selectedType.numId == 3) {
                returnDate = year + selectedType.text[0] + ' ' + month + selectedType.text[1];
            } else {
                returnDate = year + selectedType.text[0] + month;
            }
            break;
        case 'day':
            if (selectedType.numId == 3) {
                returnDate = year + selectedType.text[0] + ' ' + month + selectedType.text[1] + ' ' + day + (selectedType?.text[2] || '');
            } else {
                returnDate = year + selectedType.text[0] + month + selectedType.text[1] + day + (selectedType?.text[2] || '');
            }
            break;
        default:
            if (selectedType.numId == 3) {
                returnDate = year + selectedType.text[0] + ' ' + month + selectedType.text[1] + ' ' + day + (selectedType?.text[2] || '');
            } else {
                returnDate = year + selectedType.text[0] + month + selectedType.text[1] + day + (selectedType?.text[2] || '');
            }
            break;
    }
    return returnDate;
}

```


---

## updateDate
### example
```javascript
const CURRENT_DATE = createDateUpdater(new Date());
CURRENT_DATE('-'); //CURRENT_DATE('+'), CURRENT_DATE()
```

### code
```javascript

/**
 * @author pyeon
 * 날짜 증가/감소
 * example)))
    1.	let CURRENT_DATE = createDateUpdater(new Date());
    2.	CURRENT_DATE('-' , '+' , )
 * @param {date} currentDate  (기준 날짜(오늘))
 * @param {string} range  'year', 'month' , 'day'
 * @returns {func} dateIncDec(sort)  -> {string} : 방향 ('+' / '-' / '' -> currentDate)
 */
function createDateUpdater(currentDate, range) {
    let finalDate = currentDate; //지역변수

    function dateIncDec(sort) {  //지역변수 변경하는 함수
        const nextCalculate = {
            year: [finalDate.getFullYear() + 1, finalDate.getMonth(), finalDate.getDate()],
            month: [finalDate.getFullYear(), finalDate.getMonth() + 1, finalDate.getDate()],
            day: [finalDate.getFullYear(), finalDate.getMonth(), finalDate.getDate() + 1],
        }
        const prevCalculate = {
            year: [finalDate.getFullYear() - 1, finalDate.getMonth(), finalDate.getDate()],
            month: [finalDate.getFullYear(), finalDate.getMonth() - 1, finalDate.getDate()],
            day: [finalDate.getFullYear(), finalDate.getMonth(), finalDate.getDate() - 1],
        }

        if (sort == '+') {
            finalDate = new Date(nextCalculate[range][0], nextCalculate[range][1], nextCalculate[range][2]);
        } else if (sort == '-') {
            finalDate = new Date(prevCalculate[range][0], prevCalculate[range][1], prevCalculate[range][2]);
        }
        return finalDate;
    }
    return dateIncDec;   //함수를 return
}

```
