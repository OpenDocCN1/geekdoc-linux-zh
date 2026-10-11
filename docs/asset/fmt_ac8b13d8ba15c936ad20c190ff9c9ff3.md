
}

    e.printStackTrace();

}

```
-------------------------------------------------------------------------------------------------
// 使用 Home 接口方法生成 Remote
// 接口引用
-------------------------------------------------------------------------------------------------
public CurrentTimeSession create() {
    long startTime = 0;
    if (logging) {
        log("Calling create()");
        startTime = System.currentTimeMillis();
    }
    try {
        currentTimeSession = currentTimeSessionHome.create();
        if (logging) {
            long endTime = System.currentTimeMillis();
            log("Succeeded: create()");
            log("Execution time: " + (endTime - startTime) + " ms.");
        }
    } catch (Exception e) {
        if (logging) {
            log("Failed: create()");
        }
        e.printStackTrace();
    }
    if (logging) {
        log("Return value from create: " + currentTimeSession + ".");
    }
    return currentTimeSession;
}
```

-------------------------------------------------------------------------------------------------

// 使用 Remote 接口方法通过 bean 访问数据

-------------------------------------------------------------------------------------------------

```
public String getCurrentServerTime() {

    String returnValue = "*";

    if (currentTimeSession == null) {

        System.out.println("Error in getCurrentServerTime(): " + 

        ERROR_NULL_REMOTE);

        return returnValue;

    }

    if (logging) {

        log("Return value from getCurrentServerTime(): " + returnValue + ".");

    }

    return returnValue;

}
```

----------------------------------------------------------------------
// 工具类方法
----------------------------------------------------------------------

```java

private void log(String message) {

    if (message == null) {

        System.out.println("-- null");

        return;

    }

    if (message.length() > MAX_OUTPUT_LINE_LENGTH) {

        System.out.println("-- " + message.substring(0, MAX_OUTPUT_LINE_LENGTH) + " ...");

    } else {

        System.out.println("-- " + message);

    }

}

// 主方法

public static void main(String[] args) {

    CurrentTimeSessionTest1 client = new CurrentTimeSessionTest1();

    // 使用客户端对象调用上述的一个 Home 接口封装，

    // 创建指向 bean 的 Remote 引用。

    // 如果返回值是 Remote 接口类型，你可以直接使用客户端

    // 对象来访问远程接口方法。

    // 这部分代码由其他编写，到此为止的所有内容都是由 IDE 生成的。

    client.create();

    System.out.println(client.getCurrentServerTime());

}
```
