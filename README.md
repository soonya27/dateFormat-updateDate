# dateFormat , 날짜 증가/감소 공통처리 (전역변수 사용X, 함수내의 지역변수로 처리)

### [githubpage](https://)



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
    let finalDate = currentDate;    //

    function dateIncDec(sort) {
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
    return dateIncDec;
}

```
