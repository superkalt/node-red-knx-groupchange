![image](https://user-images.githubusercontent.com/44277174/217163827-05802995-d4d1-4550-8ba8-8cc6dba38717.png)

wenn man es besser und schneller machen kann - lasst es mich wissen


## 3 to 1

```
let _eingang = msg.knx.destination;
let _meinArray = _eingang.trim().split("/");

function _toBIN(_dec, _laenge) {
    let _muster = "0000000000000000";
    let _tempBin = parseInt(_dec).toString(2);
    let _tempBinNeu = null;
    let _davor = null;

    if (_dec.length != _laenge) {
        _davor = _muster.slice(0, _laenge - _tempBin.length);
        _tempBinNeu = _davor + _tempBin;
    } else {
        _tempBinNeu = _tempBin;
    }
    return _tempBinNeu
}

msg.knx.destinationRaw = parseInt(_toBIN(_meinArray[0], 5) + _toBIN(_meinArray[1], 3) + _toBIN(_meinArray[2], 8), 2);
node.status({ fill: "green", shape: "dot", text: msg.knx.destination + " => " + msg.knx.destinationRaw });
return msg;    
```

## 1 to 3

```
let _muster = "0000000000000000";
let _binGa = msg.destinationRaw.toString(2);
let _binGaNeu = _binGa;

if (_binGa.length != 16) {
    _muster = _muster.slice(0, 16 - _binGa.length);
    _binGaNeu = _muster + _binGa;
} 

msg.destination = parseInt(_binGaNeu.slice(0, 5), 2) + "/" + parseInt(_binGaNeu.slice(5, 8), 2) + "/" + parseInt(_binGaNeu.slice(8), 2);

node.status({fill: "green", shape: "dot", text: msg.destinationRaw + " => " + msg.destination});

return msg;
```
