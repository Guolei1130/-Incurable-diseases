问题描述链接 [Android Bug分析系列：第三方平台安装app启动后，home键回到桌面后点击app启动时会再次启动入口类bug的原因剖析](https://www.cnblogs.com/net168/p/5722752.html)

### 方法一

```
// 避免从桌面启动程序后，会重新实例化入口类的activity
if (!this.isTaskRoot()) {
    Intent intent = getIntent();
    if (intent != null) {
        String action = intent.getAction();
        if (intent.hasCategory(Intent.CATEGORY_LAUNCHER) && Intent.ACTION_MAIN.equals(action)) {
            finish();
            return;
        }
    }
}

```

### 方法二

```
Intent intent = getIntent();
    int intentFlag = intent.getFlags();
    if ((intentFlag & Intent.FLAG_ACTIVITY_BROUGHT_TO_FRONT) != 0) {
      if (intent.getAction() != null && intent.getAction()
          .equals(Intent.ACTION_MAIN)) {
        finish();
        return;
      }
    }
```

### 方法三

```
Intent intent = getIntent();
    boolean isInvalid = Intent.ACTION_MAIN.equals(intent.getAction())
        && intent.hasCategory(Intent.CATEGORY_LAUNCHER)
        && (intent.getFlags() & Intent.FLAG_ACTIVITY_BROUGHT_TO_FRONT) != 0
        && (intent.getFlags() & Intent.FLAG_ACTIVITY_RESET_TASK_IF_NEEDED) != 0;
    if (isInvalid) {
      finish();
      return;
    }
```