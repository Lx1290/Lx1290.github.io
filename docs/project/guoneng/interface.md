## 接口相关

### 分配鉴权key和密钥

AccessKey：494875a8be9643799b8cf7f9368493dd（以实际为准）
AccessSecret：e316763456cd4d319399e1dc108bc2e6（以实际为准）

### 计算sign 和 timestamp

```
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
public class TokenUtil {

    public static String SHA256(String strSrc) {return encrypt(strSrc, "SHA-256").toUpperCase(); }

    public static String encrypt(String strSrc, String algorithm) {
        MessageDigest md = null;
        String strDes = null;

        byte[] bt = strSrc.getBytes();
        try {
            md = MessageDigest.getInstance(algorithm);
            md.update(bt);
            strDes = bytes2Hex(md.digest()); //to HexString
        } catch (NoSuchAlgorithmException e) {
            System.out.println("Invalid algorithm.");
            return null;
        }
        return strDes;
    }

    public static String bytes2Hex(byte[] bts) {
        String des = "";
        String tmp = null;
        for (int i = 0; i < bts.length; i++) {
            tmp = (Integer.toHexString(bts[i] & 0xFF));
            if (tmp.length() == 1) {
                des += "0";
            }
            des += tmp;
        }
        return des;
    }

    public static void main(String[] args) {
        String accessKey = "494875a8be9643799b8cf7f9368493dd";
        String accessSecret = "e316763456cd4d319399e1dc108bc2e6";
        long timestamp = System.currentTimeMillis();
        System.out.println("timestamp : "+timestamp);
        System.out.println("sign: " + SHA256(accessKey + timestamp + accessSecret));
    }
}
```

### 获取token

- 请求方式：GET
- 请求地址：/gateway/auth/v1/api/accessToken
- 请求参数：

  | 名称      | 类型   | 是否必填 | 描述                                                        |
  | --------- | ------ | -------- | ----------------------------------------------------------- |
  | accessKey | String | Y        | accessKey                                                   |
  | timestamp | String | Y        | 时间戳                                                      |
  | sign      | String | Y        | 加密值，规则：upper(sha256(appKey + timeStamp + appSecret)) |
- 返回示例：

  ```
  {
      "code": "000000",
      "msg": "处理成功",
      "data": "76F7AF74D0614573BDB1B7E46A04EF7B",
      "time":60
  }
  ```

### 调用指标信息接口

- 请求方式：POST
- 请求地址：https://coalaiinsight.ceic.com:8180/gateway/server/api/index/getIndexInfo
- 请求参数：| 名称          | 类型   | 是否必填 | 描述                            |
  | ------------- | ------ | -------- | ------------------------------- |
  | Authorization | String | Y        | 将获取到的token值放入到header中 |
- 返回示例：
  ```
  {
  "code": "000000",
  "mesg": "处理成功",
  "time": "2025-06-10T08:40:17.486Z",
  "data": [
      {
          "indexId": 24700,
          "createTime": "2024-10-21 16:39:51",
          "updateTime": "2024-11-26 08:57:19",
          "createOriginTime": null,
          "updateOriginTime": null,
          "indexLevelOne": "03、煤炭运输",
          "indexLevelTwo": "2、运量",
          "indexLevelThree": "铁路发运量",
          "indexName": "呼和浩特铁路局总发运量",
          "indexOriginCode": "10E6DA517413ACB65AC2C3B54047BAC0",
          "indexOriginName": "",
          "areaCode": "",
          "areaName": "",
          "entityCode": "",
          "entityName": "",
          "entName": "",
          "portName": "",
          "productName": "",
          "coalClas": "",
          "coalCategory": "",
          "coalUsage": "",
          "ashLow": null,
          "ashHigh": null,
          "vdafLow": null,
          "vdafHigh": null,
          "sulfurLow": null,
          "sulfurHigh": null,
          "ashFusionLow": null,
          "ashFusionHigh": null,
          "codeticleLow": null,
          "codeticleHigh": null,
          "grindIndexLow": null,
          "grindIndexHigh": null,
          "aoyDilatationLow": null,
          "aoyDilatationHigh": null,
          "dataType": "发运量",
          "dataUnit": "万吨",
          "dataFreqCode": "",
          "dataFreq": "日度",
          "dataSourceCode": "S01",
          "dataSource": "人工填写",
          "indexDesc": "",
          "isValidData": 1,
          "des": "",
          "uniqueId": "10E6DA517413ACB65AC2C3B54047BAC0S01",
          "maintainer": "",
          "fillingCycle": 1,
          "fillingCategoryId": 19,
          "directoryId": 31,
          "indexAliasName": null,
          "indexConcatName": null,
          "formula": null,
          "qlow": null,
          "qhigh": null,
          "ghigh": null,
          "mhigh": null,
          "yvalueLow": null,
          "mlow": null,
          "glow": null,
          "yvalueHigh": null
      }
  ]
  ```

}
    ```

### 调用指标数值接口

- 请求方式：POST
- 请求地址：https://coalaiinsight.ceic.com:8180/gateway/server/api/index/getIndexValue
- 请求参数：| 名称          | 类型   | 是否必填 | 描述                            |
  | ------------- | ------ | -------- | ------------------------------- |
  | Authorization | String | Y        | 将获取到的token值放入到header中 |
  | uniqueId      | String | Y        | 指标id                          |
  | startDate     | String | N        | 数据开始时间（yyyy-MM-dd格式）  |
  | endDate       | String | N        | 数据结束时间（yyyy-MM-dd格式）  |
- 返回示例：
  ```
      {
      "code": "000000",
      "mesg": "处理成功",
      "time": "2025-06-10T08:46:06.686Z",
      "data": {
          "10E6DA517413ACB65AC2C3B54047BAC0S01": [
              {
                  "id": 10661386,
                  "createTime": "2024-10-25 18:29:34.000000",
                  "updateTime": "2024-10-25 18:29:34.000000",
                  "dataDate": "2023-12-17 00:00:00",
                  "indexId": null,
                  "lowValue": "143.438",
                  "highValue": "143.438",
                  "value": "143.438",
                  "valueDes": "",
                  "isValidData": 1,
                  "des": "",
                  "updateOriginTime": null,
                  "createOriginTime": null,
                  "uniqueId": "10E6DA517413ACB65AC2C3B54047BAC0S01"
              }
          ]
      }
  }

  ```

## 账号列表

| AccessKey                              | AccessSecret                           | 调用平台                     |
| -------------------------------------- | -------------------------------------- | ---------------------------- |
| 61b7db1350a146c88794013d0fe5bcb0       | 1715ed29112543f4879db20fb31487b2       | 总调度室                     |
| 0119505e8b70488d8a7cceed35fb24cb       | 0149d1a3a1d04bacbb3a6fd948ad681a       | 智慧销售平台                 |
| 3ab77ed7726a4359b0455394159d1d14       | 1566197b10fd41849970f7ba4168b6de       | 数据咨询                     |
| 82133eb8134f485ca879a23c6d2f31ab       | d57d5cb5dd2346a486a571172b0dfded       | 山西采购中心                 |
| ca42a5f11361401998e3228fe3c67a8e       | 8b055746e3324b4cbd9f6638b279f0ca       | 大屏                         |
| 5bd936c5b4f54091a685bc5585ad7957       | 11a3dc40542b4864991cbbd9381ec1e3       | 北方两港                     |
| fd004bfa55804408ada85beaea7d008a       | 49555f735ef243e79183c21741dc028b       | 电商平台                     |
| ~~00332ebfb9904806abc2ca3e60083d8e~~ | ~~e1d0e2c3ac254a2dbebbc4fca910079f~~ | ~~数字化转型项目（电商）~~ |
| ~~fa7bfe27fc9d497d8aea0e2f60b3c64a~~ | ~~9f7134ba906747c2921bd6559aefdd1a~~ | ~~大矿直采（电商）~~       |
| ~~7c9a1dafe264429e83af73045ced8882~~ | ~~6e1199be82c045f8a3b4c07bbecaf6f1~~ | ~~年方式（电商）~~         |
