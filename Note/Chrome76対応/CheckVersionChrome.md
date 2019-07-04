# check version
var raw = ua.match(/(C|c)hrom(e|ium)\/([0-9]+)\./);
var version = raw ? parseInt(raw[3], 10) : false;

# check isChrome
// var isChrome = /Chrome/.test(navigator.userAgent) && /Google Inc/.test(navigator.vendor);
var isChrome = !!window.chrome && (!!window.chrome.webstore || !!window.chrome.runtime);

# check isSafari
var isSafari = /constructor/i.test(window.HTMLElement) || (function (p) { return p.toString() === "[object SafariRemoteNotification]"; })(!window['safari'] || (typeof safari !== 'undefined' && safari.pushNotification));
