# Async - Await - Promise

## Demo 1

```js
/* Define a functions that return promise */
const demoApi = (callNo = 1, isApiCallOk = true, timeTaken = 5000) => {
    let obj = {
        id: callNo,
        time: timeTaken,
        message: "something went wrong"
    }
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (isApiCallOk) {
                resolve(obj);
            } else {
                reject(obj);
            }
        }, timeTaken);
    });    
}

const apiCall = async (no, isSuccess = true, responseTime = 5000) => {
    const response = await demoApi(no, isSuccess, responseTime).then((res) => {
        document.getElementById('output').innerHTML += `<label style="color: green">API NO: ${res.id}, Response Time is: ${res.time} sec.</label><br/>`;
    }).catch((err) => {
        document.getElementById('output').innerHTML += `<label style="color: red">API NO: ${err.id}, Response Time is: ${err.time} sec and it is failed by - ${err.message}</label><br/>`;
    }) 
}

const callApis = () => {
    document.getElementById('logs').innerHTML = '';
    document.getElementById('output').innerHTML = '';
    let howManyApis = parseInt(document.getElementById('callNo').value);
    let responseArr = [true, false, true, true, false];
    for (let x = 1; x <= howManyApis; x++) {
        let setTime = Math.floor(Math.random() * 10000);
        let setResp = responseArr[Math.floor(Math.random() * responseArr.length)]
        apiCall(x, setResp, setTime);
        document.getElementById('logs').innerHTML += `API: ${x} - ${setTime} - ${setResp} <br/>`;
    }
}
```
