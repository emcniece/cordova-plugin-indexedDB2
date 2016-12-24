IndexedDB plugin for Apache Cordova
==================================
Implements [Indexed Database API](http://www.w3.org/TR/IndexedDB/) support for Apache Cordova apps based on [IndexedDBShim](https://github.com/axemclion/IndexedDBShim) implementation. This is an upgraded version of the unmaintained [Microsoft/cordova-plugin-indexedDB](https://github.com/Microsoft/cordova-plugin-indexedDB).

**IndexedDBShim: [v2.2.2](https://github.com/axemclion/IndexedDBShim/blob/2df04cc3e8b2f9b3d26fcbb649080667cd4d85df/dist/indexeddbshim.min.js)**

Supports Android, iOS, Windows, and browser.

### Sample usage ###

Plugin follows [Indexed Database API](http://www.w3.org/TR/IndexedDB/) specification, no special changes are required. The following sample code creates `todo` store (if not exist) and adds new record.

    var openReq = window.indexedDB.open("sampleDatabase");
    openReq.onupgradeneeded = function (event) {
        var db = event.target.result;
        db.createObjectStore("todo", {autoIncrement: true});
    };
    openReq.onsuccess = function (event) {
        var db = event.target.result,
            sampleItem = {
                todo: "my todo item",
                added_on: new Date()
            };
        var addReq = db.transaction("todo", "readwrite").objectStore("todo").add(sampleItem);
        addReq.onsuccess = function (event) {
            console.log("Operation completed successfully");
        };
        addReq.onerror = function (event) {
            console.log("Operation failed");
        };
    }
    openReq.onerror = function (event) {
        console.log("Operation failed");
    }

### Installation Instructions ###

Plugin is [Apache Cordova CLI](http://cordova.apache.org/docs/en/edge/guide_cli_index.md.html) 3.x compliant.

1. Make sure an up-to-date version of **Node.js** is installed, then type the following command to install the [Cordova CLI](https://github.com/apache/cordova-cli):

        npm install -g cordova

2. Create a project and add the platforms you want to support:

        cordova create sampleApp
        cd sampleApp
        cordova platform add android
        cordova platform add ios

3. Add IndexedDB plugin to your project:

        cordova plugin add cordova-plugin-indexeddb2
        # or
        ionic plugin add cordova-plugin-indexeddb2 --save

4. Build and run, for example:

        cordova build android
        cordova emulate android

To learn more, read [Apache Cordova CLI Usage Guide](http://cordova.apache.org/docs/en/edge/guide_cli_index.md.html).
