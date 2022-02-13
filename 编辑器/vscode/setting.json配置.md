setting.json

```json
{
    "editor.tabSize": 2,
    "editor.formatOnType": true,
    // 每次保存自动格式化
    "editor.formatOnSave": true,
    // 开启对vue中文件错误检查
    "eslint.validate": [
        "javascript",
        "html",
        "vue"
    ],
    // 每次保存的时候将代码按eslint格式进行修复
    "eslint.format.enable": true,
    //让prettier使用eslint的代码格式进行校验
    "prettier.eslintIntegration": true, 
    //去掉代码结尾的分号
    "prettier.semi": false, 
    //使用带引号替代双引号
    "prettier.singleQuote": true, 
    //让函数(名)和后面的括号之间加个空格
    "javascript.format.insertSpaceBeforeFunctionParenthesis": true, 
    //格式化.vue中html
    "vetur.format.defaultFormatter.html": "js-beautify-html", 
    "vetur.format.defaultFormatterOptions": {
        "js-beautify-html": {
            "wrap_attributes": "force-aligned" //属性强制折行对齐
        }
    },
    "emmet.excludeLanguages": [
        "markdown"
    ],
    "workbench.startupEditor": "none",
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "explorer.confirmDelete": false,
    "explorer.confirmDragAndDrop": false,
    "security.workspace.trust.untrustedFiles": "open",
    "[vue]": {
        "editor.defaultFormatter": "octref.vetur"
    },
    "[json]": {
        "editor.defaultFormatter": "vscode.json-language-features"
    },
    "[markdown]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "workbench.editor.untitled.hint": "hidden",
    // 自定义语言模式
    "[typescript]": {
        "editor.defaultFormatter": "vscode.typescript-language-features"
    },
    "files.associations": {
        "*.conf": "bat"
    },
    "window.titleBarStyle": "custom",
    "git.ignoreMissingGitWarning": true,
    "files.autoSaveDelay": 0,
    "update.enableWindowsBackgroundUpdates": true,
    "background.customImages": [
        "file://C:/Users/11735/Pictures/王天草/3.jpg",
        // "file://C:/Users/11735/Pictures/vscode.jfif",
    ],
    "background.style": {
        "content": "''",
        "pointer-events": "none",
        "position": "absolute", //图片位置
        "max-width": "100%",
        "height": "100%",
        "z-index": "99999",
        "background.repeat": "no-repeat",
        "background-size": "100%,100%", //图片大小
        "opacity": 0.1 //透明度
    },
    "background.useFront": true,
    //是否使用默认图片
    "background.useDefault": false,
    "liveServer.settings.donotShowInfoMsg": true,
    // 重复使用图片
    "background.loop": true,
    "workbench.colorTheme": "Monokai Dimmed",
    "editor.quickSuggestions": {
        "strings": true
    },
    // 编辑器失去焦点时自动保存更新后的文件
    "files.autoSave": "onFocusChange",
    // 关闭标签介绍信息
    "editor.hover.delay": 5000,
    // 自动折行
    "editor.wordWrap": "on",
    "bracketPairColorizer.depreciation-notice": false,
}
```

