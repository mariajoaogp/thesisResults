"use strict";

var isPrerendering = !1;

function regexCheck(regexList, whiteList) {
    var txt = document.getElementsByTagName("html")[0].innerHTML, len = regexList.length, i;
    var bwLen = whiteList.length, whiteListed = !1;
    var whitelist = [ "accounts.google.com", "blocksimanager.appspot.com", "www.block.si", "www.google.com", "service2.block.si", "service.block.si", "accounts.youtube.com" ];
    var k = whitelist.length - 1;
    while (k > -1) {
        if (whitelist[k] === location.host || location.host.indexOf(whitelist[k]) > -1) whiteListed = !0;
        k--;
    }
    for (i = 0; bwLen >= i; i++) {
        if (i == bwLen) break;
        if (location.host.indexOf(whiteList[i][0]) > -1) if (0 === whiteList[i][1] || "0" === whiteList[i][1]) whiteListed = !0;
    }
    if (0 == whiteListed) for (i = 0; len > i; i++) if (txt.search(new RegExp(regexList[i], "im")) !== -1) {
        window.location.replace("http://www.block.si/regex.php?url=" + window.location.host + "&reg=" + regexList[i]);
        break;
    }
}

function handleVisibilityChange() {
    if (!isPrerendering || location.host.indexOf("block.si") > -1) return;
    chrome.runtime.sendMessage({
        regex: !0
    }, function(response) {
        regexCheck(response.Regex, response.WhiteList);
    });
    isPrerendering = !1;
}

if ("prerender" !== document.webkitVisibilityState && location.host.indexOf("block.si") === -1) chrome.runtime.sendMessage({
    regex: !0
}, function(response) {
    regexCheck(response.Regex, response.WhiteList);
}); else {
    isPrerendering = !0;
    document.addEventListener("webkitvisibilitychange", handleVisibilityChange, !1);
}

window.addEventListener("message", function(event) {
    if (event.data.type && "FROM_PAGE" === event.data.type) {
        var urlLink = document.getElementById("url_link");
        chrome.runtime.sendMessage({
            warning: event.data.text,
            url: urlLink.innerText
        });
    }
}, !1);