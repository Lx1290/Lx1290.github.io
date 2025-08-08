## 下载前端获取不到文件名

```
 public static void responseConfig(HttpServletResponse response, String fileName) throws UnsupportedEncodingException {
        response.setContentType("application/vnd.openxmlformats-officedocument.spreadsheetml.sheet");
        response.setHeader("Access-Control-Expose-Headers","Content-Disposition");
        response.setHeader("Content-Disposition", String.format("attachment;filename=%s.xlsx", URLEncoder.encode(fileName, "utf-8")));
    }
```