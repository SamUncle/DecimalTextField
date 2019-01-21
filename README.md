## DecimalTextField
#### 用来限制用户输入小数点限制的封装类继承自UITextField
#### 使用注意
使用DecimalTextFieldDelegate时，父类UITextFieldDelegate代理通过DecimalTextFieldDelegate方法实现，UITextFieldDelegate将使用无效（代理不能够继承）
#### 使用方法

1. 声明代理<DecimalTextFieldDelegate>
2. 设置代理
3. 实现代理方法
```
//MARK: --DecimalTextFieldDelegate 实现此代理方法用户限制用户输入小数
- (BOOL)decimalTextField:(DecimalTextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string hasDot:(BOOL)hasDot{


if (string.length > 0) {
// 小数点后最多能输入几位
if (hasDot) {
NSRange ran = [textField.text rangeOfString:@"."];
// 由于range.location是NSUInteger类型的，所以这里不能通过(range.location - ran.location)>2来判断
int scale = 0;
if (range.location > ran.location) {
if (textField == self.textField) {
scale = ScaleLimit;
}
if ([textField.text pathExtension].length >= scale) {

NSLog(@"只能输入%d位小数",scale);


return NO;
}
}
}
}
return YES;
}

```
