# LinkedIn-Hacks

### Unfollow all followings



```
function isHidden(el) {
    if (el) return (el.offsetParent === null);
    else return false;
}

TotalUnfollowed = 0;

var LoadingAnimation = document.getElementsByClassName("initial-load-animation")[0];
var CatchLoadingAnimation = setInterval(function() {
    if (isHidden(LoadingAnimation) == true) {
        clearInterval(CatchLoadingAnimation);
        /* START: RUN AFTER PAGE LOAD COMPLETE */
        /* SHOW STATUS AND CONFIRMATION ELEMENT */
        var LiUnfollow = document.createElement("div");
        LiUnfollow.id = "LiUnfollow";
        LiUnfollow.innerHTML = "<div style=\"color: aliceblue; background-color: #005E93; border-bottom: 1px solid #ced0d4; padding: 7.5px; text-align: center;\">LinkedIn Unfollower</div><div name=\"Confirmation\"><div style=\"font-size: 14px; color: #4b4f56; text-align: center; margin: 7.5px; display: block; cursor: default;\">Ready To Unfollow Everyone?</div><div style=\"background-color: #005E93; border-top: 1px solid #ced0d4; padding: 7.5px;\"><button type=\"button\" name=\"Continue\" style=\"background-color: #f6f7f9; color: #4b4f56; border: 1px solid #ced0d4; padding: 0 8px; line-height: 27.5px; font-weight: normal; font-family: -apple-system, system-ui, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 14px; \">Yes</button><button type=\"button\" name=\"Close\" style=\"background-color: #f6f7f9; color: #4b4f56; border: 1px solid #ced0d4; padding: 0 8px; line-height: 27.5px; font-weight: normal; font-family: -apple-system, system-ui, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 14px; margin-left: 7.5px;\">No</button></div></div><div name=\"Status\" style=\"display: none;\"><div style=\"font-size: 14px; color: #4b4f56; margin: 7.5px; display: block; cursor: default;\"><div name=\"Message\" style=\"display: none;\">Unfollowed Successfully!</div>Total Unfollowed: <span name=\"TotalUnfollowed\">0</span></div><div style=\"background-color: #005E93; border-top: 1px solid #ced0d4; padding: 7.5px;\"><button type=\"button\" name=\"Stop\" style=\"background-color: #f6f7f9; color: #4b4f56; border: 1px solid #ced0d4; padding: 0 8px; line-height: 27.5px; font-weight: normal; font-family: -apple-system, system-ui, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 14px;\">Stop</button></div></div>";
        LiUnfollow.style = "width: 300px; height: auto; background: #f6f7f9; z-index: 9999999999; position: fixed; top: calc(50% - 100px); right: calc(50% - 150px); border: 1px solid #ced0d4; border-radius: 2px; font-family: -apple-system, system-ui, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: medium; font-weight: normal;";
        document.body.appendChild(LiUnfollow);

        /* ONCLICK EVENTS */
        /* NO BUTTON */
        if (document.querySelectorAll("#LiUnfollow [name=Close]")[0]) document.querySelectorAll("#LiUnfollow [name=Close]")[0].onclick = function() {
            document.querySelectorAll("#LiUnfollow")[0].outerHTML = "";
        };

        /* YES BUTTON */
        if (document.querySelectorAll("#LiUnfollow [name=Continue]")[0]) document.querySelectorAll("#LiUnfollow [name=Continue]")[0].onclick = function() {
            document.querySelectorAll("#LiUnfollow [name=Confirmation]")[0].style.display = "none";
            document.querySelectorAll("#LiUnfollow [name=Status]")[0].style.display = "block";
            UnfollowFunction = setInterval(function() {
                var UnfollowButton = document.querySelectorAll("ul > li [data-control-name=\"actor_follow_toggle\"].is-following");
                for (var i = UnfollowButton.length - 1; i >= 0; i--) {
                    TotalUnfollowed++;
                    UnfollowButton[i].click();
                    document.querySelectorAll("#LiUnfollow [name=TotalUnfollowed]")[0].innerHTML = Number(document.querySelectorAll("#LiUnfollow [name=TotalUnfollowed]")[0].innerHTML) + 1;
                }
            }, 1000);
            ScrollToBottom = setInterval(function() {
                window.scrollBy(0, 12.5);
            }, 15);

            function CheckPageEnd(LastHeight) {
                var CurrentHeight = document.body.scrollHeight;
                if (!(CurrentHeight > LastHeight)) {
                    clearInterval(ScrollToBottom);
                    clearInterval(UnfollowFunction);
                    document.querySelectorAll("#LiUnfollow [name=Message]")[0].style.display = "block";
                    document.querySelectorAll("#LiUnfollow [name=Stop]")[0].innerHTML = "Close";
                } else setTimeout(function() {
                    CheckPageEnd(CurrentHeight);
                }, 7.5 * 1000);
            }
            CheckPageEnd(0);
        }

        /* STOP BUTTON */
        if (document.querySelectorAll("#LiUnfollow [name=Stop]")[0]) document.querySelectorAll("#LiUnfollow [name=Stop]")[0].onclick = function() {
            clearInterval(ScrollToBottom);
            clearInterval(UnfollowFunction);
            document.querySelectorAll("#LiUnfollow")[0].outerHTML = "";
        };
        /* END: RUN AFTER PAGE LOAD COMPLETE */
    }
}, 1000);

```


### Bulk connection requests


```

Linkedin = {
    config: {
        scrollDelay: 3000,
        actionDelay: 5000,
        nextPageDelay: 5000,
        // set to -1 for no limit
        maxRequests: -1,
        totalRequestsSent: 0,
        // set to true to add note in invites
        addNote: false,
        note: "I'm looking forward to connecting with you!"
    },
    init: function(data, config) {
        console.info("INFO: script initialized on the page...");
        console.debug("DEBUG: scrolling to bottom in " + config.scrollDelay + " ms");
        setTimeout(() => this.scrollBottom(data, config), config.actionDelay);
    },
    scrollBottom: function(data, config) {
        window.scrollTo({
            top: document.body.scrollHeight,
            behavior: 'smooth'
        });
        console.debug("DEBUG: scrolling to top in " + config.scrollDelay + " ms");
        setTimeout(() => this.scrollTop(data, config), config.scrollDelay);
    },
    scrollTop: function(data, config) {
        window.scrollTo({
            top: 0,
            behavior: 'smooth'
        });
        console.debug("DEBUG: inspecting elements in " + config.scrollDelay + " ms");
        setTimeout(() => this.inspect(data, config), config.scrollDelay);
    },
    inspect: function(data, config) {
        var totalRows = this.totalRows();
        console.debug("DEBUG: total search results found on page are " + totalRows);
        if (totalRows >= 0) {
            this.compile(data, config);
        } else {
            console.warn("WARN: end of search results!");
            this.complete(config);
        }
    },
    compile: function(data, config) {
        var elements = document.querySelectorAll('button');
        data.pageButtons = [...elements].filter(function(element) {
            return element.textContent.trim() === "Connect";
        });
        if (!data.pageButtons || data.pageButtons.length === 0) {
            console.warn("ERROR: no connect buttons found on page!");
            console.info("INFO: moving to next page...");
            setTimeout(() => {
                this.nextPage(config)
            }, config.nextPageDelay);
        } else {
            data.pageButtonTotal = data.pageButtons.length;
            console.info("INFO: " + data.pageButtonTotal + " connect buttons found");
            data.pageButtonIndex = 0;
            console.debug("DEBUG: starting to send invites in " + config.actionDelay + " ms");
            setTimeout(() => {
                this.sendInvites(data, config)
            }, config.actionDelay);
        }
    },
    sendInvites: function(data, config) {
        console.debug("remaining requests " + config.maxRequests);
        if (config.maxRequests == 0) {
            console.info("INFO: max requests reached for the script run!");
            this.complete(config);
        } else {
            console.debug('DEBUG: sending invite to ' + (data.pageButtonIndex + 1) + ' out of ' + data.pageButtonTotal);
            var button = data.pageButtons[data.pageButtonIndex];
            button.click();
            if (config.addNote && config.note) {
                console.debug("DEBUG: clicking Add a note in popup, if present, in " + config.actionDelay + " ms");
                setTimeout(() => this.clickAddNote(data, config), config.actionDelay);
            } else {
                console.debug("DEBUG: clicking done in popup, if present, in " + config.actionDelay + " ms");
                setTimeout(() => this.clickDone(data, config), config.actionDelay);
            }
        }
    },
    clickAddNote: function(data, config) {
        var buttons = document.querySelectorAll('button');
        var addNoteButton = Array.prototype.filter.call(buttons, function(el) {
            return el.textContent.trim() === 'Add a note';
        });
        // adding note if required
        if (addNoteButton && addNoteButton[0]) {
            console.debug("DEBUG: clicking add a note button to paste note");
            addNoteButton[0].click();
            console.debug("DEBUG: pasting note in " + config.actionDelay);
            setTimeout(() => this.pasteNote(data, config), config.actionDelay);
        } else {
            console.debug("DEBUG: add note button not found, clicking send on the popup in " + config.actionDelay);
            setTimeout(() => this.clickDone(data, config), config.actionDelay);
        }
    },
    pasteNote: function(data, config) {
        noteTextBox = document.getElementById("custom-message")
        noteTextBox.value = config.note;
        noteTextBox.dispatchEvent(new Event('input', {
            bubbles: true
        }));
        console.debug("DEBUG: clicking send in popup, if present, in " + config.actionDelay + " ms");
        setTimeout(() => this.clickDone(data, config), config.actionDelay);
    },
    clickDone: function(data, config) {
        var buttons = document.querySelectorAll('button');
        var doneButton = Array.prototype.filter.call(buttons, function(el) {
            return el.textContent.trim() === 'Send';
        });
        // Click the first send button
        if (doneButton && doneButton[0]) {
            console.debug("DEBUG: clicking send button to close popup");
            doneButton[0].click();
        } else {
            console.debug("DEBUG: send button not found, clicking close on the popup in " + config.actionDelay);
        }
        setTimeout(() => this.clickClose(data, config), config.actionDelay);
    },
    clickClose: function(data, config) {
        var closeButton = document.getElementsByClassName('artdeco-modal__dismiss artdeco-button artdeco-button--circle artdeco-button--muted artdeco-button--2 artdeco-button--tertiary ember-view');
        if (closeButton && closeButton[0]) {
            closeButton[0].click();
        }
        console.info('INFO: invite sent to ' + (data.pageButtonIndex + 1) + ' out of ' + data.pageButtonTotal);
        config.maxRequests--;
        config.totalRequestsSent++;
        if (data.pageButtonIndex === (data.pageButtonTotal - 1)) {
            console.debug("DEBUG: all connections for the page done, going to next page in " + config.actionDelay + " ms");
            setTimeout(() => this.nextPage(config), config.actionDelay);
        } else {
            data.pageButtonIndex++;
            console.debug("DEBUG: sending next invite in " + config.actionDelay + " ms");
            setTimeout(() => this.sendInvites(data, config), config.actionDelay);
        }
    },
    nextPage: function(config) {
        var pagerButton = document.getElementsByClassName('artdeco-pagination__button--next');
        if (!pagerButton || pagerButton.length === 0) {
            console.info("INFO: no next page button found!");
            return this.complete(config);
        }
        console.info("INFO: Going to next page...");
        pagerButton[0].children[0].click();
        setTimeout(() => this.init({}, config), config.nextPageDelay);
    },
    complete: function(config) {
        console.info('INFO: script completed after sending ' + config.totalRequestsSent + ' connection requests');
    },
    totalRows: function() {
        var search_results = document.getElementsByClassName('search-result');
        if (search_results && search_results.length != 0) {
            return search_results.length;
        } else {
            return 0;
        }
    }
}

Linkedin.init({}, Linkedin.config);

```

### Accept all connection requests

```
var x = document.getElementsByClassName('invitation-card__action-btn artdeco-button artdeco-button--2 artdeco-button--secondary ember-view');
for (var i = 0; i < x.length; i++) x[i].click();
```

### Withdraw all unaccepted connection requests
```
var Allbuttons = document.querySelectorAll('button');
var withdrawButtons = Array.prototype.filter.call(buttons, function (el) {
    return el.textContent.trim() === 'Withdraw';
});

var withdrawRecursively = (index) => {
    if (index === withdrawButtons.length) {
        alert("All connections withdrawn on the page!");
        checkNextPage();
    } else {
        withdrawButtons[index].click();
        setTimeout(() => clickNewWithdraw(index), 1000);
    }
}

var clickNewWithdraw = (index) => {
    var AllButtons = document.querySelectorAll('button');
    var newWithdrawButtons = Array.prototype.filter.call(AllButtons, function (el) {
        return el.textContent.trim() === 'Withdraw' && !withdrawButtons.includes(el);
    });
    newWithdrawButtons[0].click();
    setTimeout(() => withdrawRecursively(index+1), 1000);
}
```



