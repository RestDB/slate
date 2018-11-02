# Custom routes
bla bla routes

```js
// #!/javascript

const getData = (path) => {
    return new Promise((resolve, reject) => {
        db.get(path, {}, {$max: 10}, function(err,data){
            if (!err) {
                log.debug("Resolve", data.length);
                resolve(data);
            } else {
                log.error(err)
                reject(err);
            }    
        })
  });
}

async function onGET(req, res) {
    var ppl = await getData("/rest/people");
    var loc = await getData("/rest/locations");
    var comp = await getData("/rest/companies");
    res.end({text: JSON.stringify({people: ppl, loc: loc, corp: comp}, null, '  ')}); 
}
```
