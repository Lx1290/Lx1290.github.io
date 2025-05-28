# 数据集成

## 设置header

```
public HttpEntity setHeader(){
    HttpHeaders headers = new HttpHeaders();
    headers.set("Client-Id", urlBaseConfig.getClientId());

    JSONObject respObj = restTemplate.getForObject(urlBaseConfig.getIdssapi() + "/getToken?clientId=" + urlBaseConfig.getClientId(),JSONObject.class);
    if (Objects.requireNonNull(respObj).getInteger("code") == 0){
        headers.set("token", respObj.getString("info"));
    }
    return new HttpEntity<>(headers);
}
```

## 发送请求

```
public JSONObject idssRes(String url, HttpMethod method) {
    JSONObject respObj = restTemplate.exchange(
            urlBaseConfig.getIdssapi() + url, method, setHeader(),JSONObject.class).getBody();
    if(Objects.requireNonNull(respObj).getInteger("code") == 0){
        return respObj.getJSONObject("info");
    }
    return null;
}
```