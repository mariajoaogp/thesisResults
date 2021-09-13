
function get_spaces_for_string(str) {
    rtn = "";
    i = 7;
    while (i > str.length * 2) {
        i--;
        rtn += "";
    }
    return rtn;
}

$(function() {
    VKBBase.start();
});

VKBBase = {
    start: function() {
        chrome.tabs.onUpdated.addListener(VKBBase.update);
        chrome.tabs.onSelectionChanged.addListener(VKBBase.update);
        chrome.windows.onFocusChanged.addListener(VKBBase.update);
        if (!localStorage["badgeCounter"]) {
            localStorage["badgeCounter"] = "on";
        }
        if (!localStorage["contextMenuButton"]) {
            localStorage["contextMenuButton"] = "on";
        }
        if (localStorage["contextMenuButton"] == "on") {
            var contextMenuButton = chrome.contextMenus.create({
                "title": "Рассказать друзьям",
                "contexts": ["selection"],
                "onclick": VKBBase.selectionPost
            });
        }
        if (!localStorage["Authorized"]) {
            localStorage["Authorized"] = "no";
        }
        if (typeof localStorage['version'] == 'undefined') {
            this.onInstall();
        }
        VKBBase.set_badge_color();
    },
    get_count: function(url, tab) {
        var count_url = "https://vk.com/share.php?act=count&index=0&url=" + url;
        $.ajax({
            url: count_url,
            type: "GET",
            dataType: "html",
            success: function(data) {
                var count0 = "";
                var trigger = 0;
                var i = 0;
                while (1) {
                    if (data[i - 2] == ',' && data[i - 1] == ' ') trigger = 1;
                    if (trigger == 1) count0 += data[i];
                    i++;
                    if ((data[i] == ')' && data[i + 1] == ';') || i > 100) break;
                }
                var count = parseInt(count0);
                if (count) {
                    if (count >= 1000000) {
                        count = Math.round(count / 1000000) + "M";
                    } else if (count >= 10000) {
                        count = Math.round(count / 1000) + "k";
                    }
                }
                VKBBase.set_badge_text(count);
            },
            error: function() {
                VKBBase.set_badge_text("Oops");
            }
        });
    },
    set_badge_color: function(tabid) {
        obj = {
            color: [36, 107, 150, 255]
        }
        chrome.browserAction.setBadgeBackgroundColor(obj);
    },
    set_badge_text: function(text, tab_id) {
        if (parseInt(text) == 0 || !parseInt(text) || parseInt(text) == "" || !text) text = "";
        obj = {
            "text": get_spaces_for_string(text + "") + text,
        }
        if (tab_id) {
            obj.tabId = tab_id;
        }
        chrome.browserAction.setBadgeText(obj);
    },

    update: function(tabId, changeInfo, tab) {
        chrome.windows.getCurrent(function(w) {
            chrome.tabs.getSelected(w.id, function(tab) {
                if (localStorage["badgeCounter"] == "on") {
                    VKBBase.get_count(tab.url, tab);
                }
                chrome.browserAction.onClicked.addListener(function(tab) {
                    VKBBase.popup(tab);
                });
            })
        });
    },
    popup: function(tab) {
        var message = tab.title;
        var widgetUrl = 'https://vk.com/share.php';
        widgetUrl += '?Share_VK';
        widgetUrl += '&url=' + encodeURIComponent(tab.url);
        var W = 800,
            d = 400;
        var Z = screen.height;
        var Y = screen.width;
        var X = Math.round((Y / 2) - (W / 2));
        var c = 0;
        var p = window.open(widgetUrl, 'VK_button', "left=" + X + ",top=" + c + ",width=" + W + ",height=" + d + ",personalbar=no,toolbar=no,scrollbars=yes,location=yes,resizable=yes");
        if (p) {
            p.focus();
        }
    },
    selectionPost: function(info, tab) {
        //VKBBase.vkAuth();
        var widgetUrl = 'https://vk.com/share.php';
        widgetUrl += '?Share_VK';
        widgetUrl += '&title=' + encodeURIComponent(info.selectionText);
        var W = 800,
            d = 400;
        var Z = screen.height;
        var Y = screen.width;
        var X = Math.round((Y / 2) - (W / 2));
        var c = 0;
        var p = window.open(widgetUrl, 'VK_button', "left=" + X + ",top=" + c + ",width=" + W + ",height=" + d + ",personalbar=no,toolbar=no,scrollbars=yes,location=yes,resizable=yes");
        if (p) {
            p.focus();
        }
    },
    save_options: function() {
        if (document.getElementById("badgeCounter").checked == true) {
            localStorage["badgeCounter"] = "on";
        } else {
            localStorage["badgeCounter"] = "off";
        }
        if (document.getElementById("contextMenuButton").checked == true) {
            localStorage["contextMenuButton"] = "on";
            if (!contextMenuButton) {
                var contextMenuButton = chrome.contextMenus.create({
                    "title": "Рассказать друзьям",
                    "contexts": ["selection"],
                    "onclick": VKBBase.selectionPost
                });
            }
        } else {
            localStorage["contextMenuButton"] = "off";
            chrome.contextMenus.removeAll();
        }
        VKBBase.set_badge_text();
    },
    restore_options: function() {
        if (localStorage["badgeCounter"] == "on") {
            $("#badgeCounter").attr('checked', 'checked');
        } else {
            $("#badgeCounter").removeAttr('checked');
        }
        if (localStorage["contextMenuButton"] == "on") {
            $("#contextMenuButton").attr('checked', 'checked');
        } else {
            $("#contextMenuButton").removeAttr('checked');
        }
    },
    onInstall: function() {
        console.log("Extension Installed");
        chrome.tabs.create({
            "url": "about.html"
        });
        localStorage["version"] = VKBBase.getVersion();
    },

    onUpdate: function() {
        console.log("Extension Updated");
    },

    getVersion: function() {
        var details = chrome.app.getDetails();
        return details.version;
    },
}
