# mybatis

## 循环Map

```
<delete id="removeData" parameterType="java.util.Map">
    delete from divisor_data_clean where
    <foreach collection="removeData.keys" separator="or" item="modelId" index="index">
        (modelId = #{modelId} AND divisorId IN
        <foreach collection="removeData[modelId]" item="divisorId" open="(" separator="," close=")">
            #{divisorId}
        </foreach>)
    </foreach>
</delete>
```