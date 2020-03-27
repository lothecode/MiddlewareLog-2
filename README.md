# A Middleware to log time-stamps, HTTP method, and path
This is a middleware to log date, time, HTTP method and url in Node.js/Express environment

## Usage
### Just put this part in the app.js before routes
```javascript
// -- A Middleware to log date, time, HTTP method, path and response time
app.use((req, res, next) => {
  const startTime = Date.now()
  const today = new Date
  const dataValues = [
    today.getFullYear(),
    today.getMonth() + 1,
    today.getDate(),
  ]
  const timeValues = [
    today.getHours(),
    today.getMinutes(),
    today.getSeconds(),
  ]
  const listdate = dataValues.map(d => {
    if (d < 10) {
      d = `0${d}`
    }
    return d
  })
  const listtime = timeValues.map(t => {
    if (t < 10) {
      t = `0${t}`
    }
    return t
  })
  res.on('finish', () => {
    const finishTime = Date.now()
    const duration = finishTime - startTime
    console.log(listdate.join('-'), listtime.join(':'), '|', req.method, 'from', req.path, '|', 'total time:', `${duration}ms`)
  })
  return next()
})
// -- middleware end
```

### You can see log from terminal:
> 2020-03-27 14:54:02 | GET from / | total time: 13ms

## Environment
### Make sure to install Express.js 