# parsii

## 引入parsii依赖

```
<dependency>
    <groupId>com.scireum</groupId>
    <artifactId>parsii</artifactId>
    <version>4.0</version>
</dependency>
```

## 解析表达式

```
Scope scope = new Scope();
Variable variable = scope.getVariable("A");
variable.setValue(1);
Expression expr = null;
try {
    expr = Parser.parse("A + 5", scope);
} catch (ParseException e) {
    throw new RuntimeException(e);
}
system.out.println(expr.evaluate());
```
