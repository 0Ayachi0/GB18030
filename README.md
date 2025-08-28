# GB18030 编码库

这是一个用 MoonBit 语言实现的完整 GB18030 编码和解码库。GB18030 是中国国家标准，支持中文、日文、韩文等多种字符的编码。

## 功能特性

- ✅ 完整的 GB18030 编码和解码支持
- ✅ ASCII 字符兼容性
- ✅ 中文字符支持（一级汉字、二级汉字）
- ✅ 用户自定义区域支持
- ✅ 四字节序列支持
- ✅ Unicode 和 GB18030 码点转换
- ✅ 错误处理和验证
- ✅ 工具函数（字符统计、长度计算等）
- ✅ 完整的测试覆盖

## 主要函数

### 编码和解码
- `encode_from_string(s: String) -> Result[Array[Int], EncodeError]` - 将字符串编码为 GB18030 字节数组
- `decode_to_string(bytes: Array[Int]) -> Result[String, DecodeError]` - 将 GB18030 字节数组解码为字符串
- `encode(s: String) -> Result[Int, EncodeError]` - 编码字符串并返回字符数
- `decode(bytes: Array[Int]) -> Result[Int, DecodeError]` - 解码字节数组并返回字符数

### Unicode 转换
- `gb18030_to_unicode(gb_code: Int) -> Int` - GB18030 码点转 Unicode 码点
- `unicode_to_gb18030(unicode: Int) -> Int` - Unicode 码点转 GB18030 码点

### 验证函数
- `is_ascii(b: Int) -> Bool` - 检查字节是否为 ASCII
- `is_gb18030_lead(b: Int) -> Bool` - 检查是否为 GB18030 首字节
- `is_gb18030_trail(b: Int) -> Bool` - 检查是否为 GB18030 尾字节
- `is_valid_gb18030(bytes: Array[Int]) -> Bool` - 验证 GB18030 字节序列

### 工具函数
- `get_gb18030_length(s: String) -> Int` - 计算字符串的 GB18030 字节长度
- `contains_chinese(s: String) -> Bool` - 检查字符串是否包含中文字符
- `count_ascii_chars(s: String) -> Int` - 统计 ASCII 字符数
- `count_chinese_chars(s: String) -> Int` - 统计中文字符数

## 安装和使用

### 安装 MoonBit

首先确保已安装 MoonBit 开发环境。

### 运行测试

```bash
moon test
```

### 构建项目

```bash
moon build
```

## 使用示例

```moonbit
// 基本编码解码
let test_string = "Hello 世界！"
let encode_result = encode_from_string(test_string)
match encode_result {
    Ok(bytes) => {
        let decode_result = decode_to_string(bytes)
        match decode_result {
            Ok(decoded) => {
                // 使用解码后的字符串
                println(decoded)
            }
            Err(error) => {
                // 处理解码错误
                println("解码失败")
            }
        }
    }
    Err(error) => {
        // 处理编码错误
        println("编码失败")
    }
}

// Unicode 转换
let unicode_char = 0x4E00  // "一" 的 Unicode 码点
let gb18030_code = unicode_to_gb18030(unicode_char)
let back_to_unicode = gb18030_to_unicode(gb18030_code)

// 工具函数
let mixed_string = "Hello世界"
let ascii_count = count_ascii_chars(mixed_string)
let chinese_count = count_chinese_chars(mixed_string)
let has_chinese = contains_chinese(mixed_string)
```

## 测试覆盖

项目包含完整的测试套件，覆盖以下场景：

- ✅ 基本功能测试
- ✅ ASCII 字符检查
- ✅ GB18030 字节验证
- ✅ Unicode 映射测试
- ✅ 字符串编码测试
- ✅ 错误处理测试
- ✅ 工具函数测试

运行测试：
```bash
moon test --verbose
```

## 技术细节

### GB18030 编码结构

1. **单字节区域** (0x00-0x7F): ASCII 兼容
2. **双字节区域** (0x8140-0xFEFE): 中文、日文、韩文字符
3. **四字节区域** (0x81308130-0x84318539): 扩展字符

### 错误处理

- `DecodeError::InvalidByteSequence` - 无效的字节序列
- `DecodeError::IncompleteByteSequence` - 不完整的字节序列
- `DecodeError::OutOfRange` - 超出范围的码点
- `EncodeError::UnsupportedCharacter` - 不支持的字符
- `EncodeError::OutOfRange` - 超出范围的码点

## 许可证

本项目采用 MIT 许可证。

## 贡献

欢迎提交 Issue 和 Pull Request！

## 相关链接

- [GB18030 标准](https://en.wikipedia.org/wiki/GB_18030)
- [MoonBit 语言](https://www.moonbitlang.com/)
- [Unicode 标准](https://unicode.org/) 