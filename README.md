<!DOCTYPE html>
<html>
<head>
  <title>My Browser</title>
  <style>
    body {
      margin: 0;
      font-family: Arial;
      background: #121212;
      color: white;
    }

    #tabs {
      display: flex;
      background: #1f1f1f;
      padding: 5px;
    }

    .tab {
      padding: 8px;
      margin-right: 5px;
      background: #333;
      cursor: pointer;
    }

    .tab.active {
      background: #555;
    }

    #controls {
      display: flex;
      padding: 5px;
      background: #222;
    }

    input {
      flex: 1;
      padding: 8px;
      background: #333;
      color: white;
      border: none;
    }

    button {
      padding: 8px;
      margin-left: 5px;
      background: #444;
      color: white;
      border: none;
      cursor: pointer;
    }

    iframe {
      width: 100%;
      height: 90vh;
      border: none;
    }
  </style>
</head>
<body>

<div id="tabs"></div>

<div id="controls">
  <input id="url" placeholder="Enter URL...">
  <button onclick="go()">Go</button>
  <button onclick="newTab()">+</button>
</div>

<iframe id="view"></iframe>

<script>
let tabs = [];
let currentTab = 0;

function newTab() {
  tabs.push("https://example.com");
  currentTab = tabs.length - 1;
  renderTabs();
  load();
}

function renderTabs() {
  let tabDiv = document.getElementById("tabs");
  tabDiv.innerHTML = "";

  tabs.forEach((tab, i) => {
    let t = document.createElement("div");
    t.className = "tab" + (i === currentTab ? " active" : "");
    t.innerText = "Tab " + (i + 1);
    t.onclick = () => {
      currentTab = i;
      renderTabs();
      load();
    };
    tabDiv.appendChild(t);
  });
}

function go() {
  let url = document.getElementById("url").value;
  if (!url.startsWith("http")) {
    url = "https://" + url;
  }

  // Basic ad block (blocks some known ad domains)
  if (url.includes("ads") || url.includes("tracker")) {
    alert("Blocked ad/tracker!");
    return;
  }

  tabs[currentTab] = url;
  load();
}

function load() {
  document.getElementById("view").src = tabs[currentTab];
}

newTab();
</script>

</body>
</html>
