# android-file-template-live-template-sample

## Android live templete for Intent

```java
fun get$PREFIX$Intent(context: Context, $PARAM1$: $DATATYPE1$, $PARAM2$: $DATATYPE2$): Intent {
        Intent(context, $ACTIVITY$::class.java)
        intent.`package` = context.packageName
        intent.putExtra($NAME1$, $PARAM1$)
        intent.putExtra($NAME2$, $PARAM2$)
        return intent
    }
```
