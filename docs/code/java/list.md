# list

## 排序

```
//正序
result.stream().sorted(Comparator.comparing(item->item.get("month").toString())).collect(Collectors.toList());

//倒叙
mediaData.stream().sorted(Comparator.comparing(item->((JSONObject) item).getInteger("favTime")).reversed()).collect(Collectors.toList());
```

## JSONArray stream

```
productList.stream()
.filter(item-> finalProductList.contains(((JSONObject)item).getInteger("productId")))
.collect(Collectors.toCollection(JSONArray::new));
```

## List stream去重

```
//根据id去重
items = items.stream()
.collect(Collectors.collectingAndThen(Collectors.toCollection(() ->
        new TreeSet<>(Comparator.comparing(s ->s.getString("id")))), ArrayList::new));
```

## List 分组

```
dataList = dataList.stream() .collect(Collectors.groupingBy(item -> item.getString("dataMine")))
```

## 分组后取部分字段

```
//根据列名分组  
Map<String,List<String>> colGroupMap = itemList.stream()  
        .collect(Collectors.groupingBy(MeetColumnItem::getDataName,  
                Collectors.mapping(map -> String.valueOf(map.getDataId()), Collectors.toList())));
```