###3 to 1

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
};

msg.knx.destinationRaw = parseInt(_toBIN(_meinArray[0], 5) + _toBIN(_meinArray[1], 3) + _toBIN(_meinArray[2], 8), 2);

node.status({ fill: "green", shape: "dot", text: msg.knx.destination + " => " + msg.knx.destinationRaw });

return msg;    
