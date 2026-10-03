```python
<|DSML|thinking>
thinking_content
</|DSML|thinking>
<|DSML|tool_calls>
  <|DSML|invoke name="$TOOL_NAME">
    <|DSML|parameter name="$PARAMETER_NAME" string="true|false">$PARAMETER_VALUE
    </|DSML|parameter>
    ...
  </|DSML|invoke>
</|DSML|tool_calls>
```
