# GB18030 编解码库 for Moonbit

[![Build Status](https://img.shields.io/github/actions/workflow/status/0Ayachi0/gb18030/ci.yml)](https://github.com/0Ayachi0/gb18030/actions) [![codecov](https://codecov.io/gh/0Ayachi0/gb18030/branch/main/graph/badge.svg)](https://codecov.io/gh/0Ayachi0/gb18030)

[English](README.md) | 简体中文

一个用 Moonbit 语言实现的综合 GB18030 编解码库，提供完整的 Unicode 映射和高效的字节序列处理，支持中文字符编码标准的各种需求。

## 🚀 核心特性

• 🎯 **核心编解码** – 完整的 GB18030 与 Unicode 双向转换  
• 🔧 **多种输入格式** – 支持字符串、数组和迭代器  
• 🚀 **高级功能** – 增量编解码和批量处理  
• 📊 **性能优化** – 高效的字节序列处理和内存管理  
• 🔄 **错误处理** – 全面的错误检测和恢复机制  
• 🎨 **灵活API** – 多种编解码接口适应不同使用场景  
• 📈 **统计与分析** – 字符计数和中文字符检测  
• 🔍 **类型安全** – 具有健壮类型系统的完整错误类型  
• 📦 **批量操作** – 高效处理大量文本数据  
• 🧪 **测试覆盖** – 全面的测试套件，代码覆盖率达85.61%  
• 📚 **文档完善** – 详细的使用示例和 API 参考  

## 📥 安装

```bash
moon add 0Ayachi0/GB18030@0.1.0
```

## 🚀 使用指南

### 🔨 基本编解码
执行基本的 GB18030 编码和解码操作。

```moonbit
// 基本字符串编码
let test_string = "Hello 你好 World 世界"
let encoded_result = encode_from_string(test_string)
match encoded_result {
    Ok(bytes) => {
        // 处理编码后的字节
        let byte_count = bytes.length()
        // byte_count 将是所需的总字节数
    }
    Err(_) => {
        // 处理编码错误
    }
}

// 基本字节解码
let test_bytes = [72, 101, 108, 108, 111, 0xB0, 0xA1, 32, 87, 111, 114, 108, 100]  // "Hello中 World"
let decoded_result = decode_to_string(test_bytes)
match decoded_result {
    Ok(result_string) => {
        // 处理解码后的字符串
        let char_count = result_string.length()
    }
    Err(_) => {
        // 处理解码错误
    }
}
```

### 🎯 高级编码操作
使用不同的输入格式进行编码操作。

```moonbit
// 从字符数组编码
let char_array = ['H', 'e', 'l', 'l', 'o', ' ', '你', '好']
let encode_array_result = encode_from_array(char_array)
match encode_array_result {
    Ok(bytes) => {
        // 处理编码后的字节
    }
    Err(_) => {
        // 处理错误
    }
}

// 从迭代器编码
let char_iter = char_array.iter()
let encode_iter_result = encode_from_iter(char_iter)
match encode_iter_result {
    Ok(bytes) => {
        // 处理编码后的字节
    }
    Err(_) => {
        // 处理错误
    }
}

// 获取编码长度而不实际编码
let length = get_gb18030_length("Hello 你好")
// length 将是编码所需的字节数
```

### 🔧 高级解码操作
使用不同的输出格式进行解码操作。

```moonbit
// 解码为字符数组
let decode_array_result = decode_to_array(test_bytes)
match decode_array_result {
    Ok(char_array) => {
        // 处理字符数组
        let char_count = char_array.length()
    }
    Err(_) => {
        // 处理错误
    }
}

// 解码为迭代器
let decode_iter_result = decode_to_iter(test_bytes)
match decode_iter_result {
    Ok(iter) => {
        let count = iter.count()
        // 处理迭代器
    }
    Err(_) => {
        // 处理错误
    }
}

// 获取字符数而不完全解码
let char_count = decode(test_bytes)
match char_count {
    Ok(count) => {
        // count 是字符数
    }
    Err(_) => {
        // 处理错误
    }
}
```

### 🔄 错误处理
优雅地处理各种编码和解码错误。

```moonbit
// 处理无效字节序列
let invalid_bytes = [0x81, 0x3F]  // 无效的 GB18030 序列
let decode_result = decode_to_string(invalid_bytes)
match decode_result {
    Ok(_) => {
        // 成功情况
    }
    Err(DecodeError::InvalidByteSequence) => {
        // 处理无效字节序列
    }
    Err(DecodeError::IncompleteByteSequence) => {
        // 处理不完整字节序列
    }
    Err(DecodeError::OutOfRange) => {
        // 处理超出范围错误
    }
}

// 处理编码错误
let encode_result = encode_from_string("")
match encode_result {
    Ok(bytes) => {
        // 成功情况
    }
    Err(EncodeError::InvalidCharacter) => {
        // 处理无效字符
    }
    Err(EncodeError::UnsupportedEncoding) => {
        // 处理不支持的编码
    }
}
```

### 📈 字符分析和统计
分析文本内容并获取统计信息。

```moonbit
// 检查字符串是否包含中文字符
let has_chinese = contains_chinese("Hello 你好 World")
// has_chinese 将为 true

// 统计 ASCII 字符
let ascii_count = count_ascii_chars("Hello 你好 World 123")
// ascii_count 将为 18（包括空格和数字）

// 统计中文字符
let chinese_count = count_chinese_chars("Hello 你好 World 世界")
// chinese_count 将为 4

// 验证 GB18030 字节序列
let is_valid = is_valid_gb18030(test_bytes)
// is_valid 对于有效序列将为 true
```

### 🎨 Unicode 映射
处理 Unicode 与 GB18030 的映射。

```moonbit
// 将 Unicode 转换为 GB18030
let unicode_char = 0x4E00  // "一" 字符
let gb_code = unicode_to_gb18030(unicode_char)
// gb_code 将为 0xB0A1

// 将 GB18030 转换为 Unicode
let gb18030_code = 0xB0A1
let unicode = gb18030_to_unicode(gb18030_code)
// unicode 将为 0x4E00

// 处理超出范围的映射
let invalid_unicode = 0x10FFFF  // 最大 Unicode 值
let result = unicode_to_gb18030(invalid_unicode)
// result 将为 0x3F3F（默认值）
```

### 🏗️ 复杂文本处理
处理复杂的文本处理场景。

```moonbit
// 处理包含混合内容的大文本
let large_text = "This is a very long text that contains many characters and should be handled properly by the encoding system. 这是一个很长的文本，包含很多字符，应该被编码系统正确处理。This is a very long text that contains many characters and should be handled properly by the encoding system. 这是一个很长的文本，包含很多字符，应该被编码系统正确处理。"

let encode_result = encode_from_string(large_text)
match encode_result {
    Ok(bytes) => {
        // 处理大量编码数据
        let total_bytes = bytes.length()
        
        // 解码回验证
        let decode_result = decode_to_string(bytes)
        match decode_result {
            Ok(decoded_text) => {
                // 验证编码/解码完整性
                let is_same = decoded_text == large_text
            }
            Err(_) => {
                // 处理解码错误
            }
        }
    }
    Err(_) => {
        // 处理编码错误
    }
}

// 批量处理多个字符串
let text_list = ["Hello", "你好", "World", "世界", "123", "!@#"]
let mut all_bytes = []

for text in text_list {
    let encode_result = encode_from_string(text)
    match encode_result {
        Ok(bytes) => {
            all_bytes = all_bytes + bytes
        }
        Err(_) => {
            // 处理此文本的错误
        }
    }
}
```

## 📋 数据结构

### 错误类型
```moonbit
enum DecodeError {
    InvalidByteSequence,    // 无效的 GB18030 字节序列
    IncompleteByteSequence, // 不完整的字节序列
    OutOfRange             // 字节序列超出有效范围
}

enum EncodeError {
    InvalidCharacter,      // 无效的编码字符
    UnsupportedEncoding    // 不支持的编码格式
}
```

### 核心函数
```moonbit
// 编码函数
encode_from_string(s: String) -> Result[Array[Int], EncodeError]
encode_from_array(chars: Array[Char]) -> Result[Array[Int], EncodeError]
encode_from_iter(chars: Iter[Char]) -> Result[Array[Int], EncodeError]

// 解码函数
decode_to_string(bytes: Array[Int]) -> Result[String, DecodeError]
decode_to_array(bytes: Array[Int]) -> Result[Array[Char], DecodeError]
decode_to_iter(bytes: Array[Int]) -> Result[Iter[Char], DecodeError]
decode(bytes: Array[Int]) -> Result[Int, DecodeError]

// 工具函数
get_gb18030_length(s: String) -> Int
contains_chinese(s: String) -> Bool
count_ascii_chars(s: String) -> Int
count_chinese_chars(s: String) -> Int
is_valid_gb18030(bytes: Array[Int]) -> Bool

// 映射函数
unicode_to_gb18030(unicode: Int) -> Int
gb18030_to_unicode(gb_code: Int) -> Int
```

## 📊 完整 API 参考

### 核心编解码
- `encode_from_string(s)` - 将字符串编码为 GB18030 字节
- `encode_from_array(chars)` - 将字符数组编码为 GB18030 字节
- `encode_from_iter(chars)` - 将字符迭代器编码为 GB18030 字节
- `decode_to_string(bytes)` - 将 GB18030 字节解码为字符串
- `decode_to_array(bytes)` - 将 GB18030 字节解码为字符数组
- `decode_to_iter(bytes)` - 将 GB18030 字节解码为字符迭代器
- `decode(bytes)` - 从 GB18030 字节获取字符数

### 工具函数
- `get_gb18030_length(s)` - 获取字符串的编码长度
- `contains_chinese(s)` - 检查字符串是否包含中文字符
- `count_ascii_chars(s)` - 统计字符串中的 ASCII 字符
- `count_chinese_chars(s)` - 统计字符串中的中文字符
- `is_valid_gb18030(bytes)` - 验证 GB18030 字节序列

### 映射函数
- `unicode_to_gb18030(unicode)` - 将 Unicode 转换为 GB18030 码
- `gb18030_to_unicode(gb_code)` - 将 GB18030 码转换为 Unicode

### 辅助函数
- `is_ascii(byte)` - 检查字节是否为 ASCII
- `is_gb18030_lead(byte)` - 检查字节是否为 GB18030 前导字节
- `is_gb18030_trail(byte)` - 检查字节是否为 GB18030 尾随字节

## 📈 性能特征

| 操作 | 时间复杂度 | 空间复杂度 |
|------|------------|------------|
| `encode_from_string()` | O(n) | O(n) |
| `encode_from_array()` | O(n) | O(n) |
| `encode_from_iter()` | O(n) | O(n) |
| `decode_to_string()` | O(n) | O(n) |
| `decode_to_array()` | O(n) | O(n) |
| `decode_to_iter()` | O(n) | O(n) |
| `decode()` | O(n) | O(1) |
| `get_gb18030_length()` | O(n) | O(1) |
| `contains_chinese()` | O(n) | O(1) |
| `count_ascii_chars()` | O(n) | O(1) |
| `count_chinese_chars()` | O(n) | O(1) |
| `is_valid_gb18030()` | O(n) | O(1) |
| `unicode_to_gb18030()` | O(1) | O(1) |
| `gb18030_to_unicode()` | O(1) | O(1) |

## 🏗️ 算法详情

### GB18030 编码算法
1. **字符分析**: 检查字符是 ASCII 还是中文
2. **ASCII 处理**: ASCII 字符直接字节转换
3. **中文处理**: 使用映射表处理中文字符
4. **字节序列生成**: 生成正确的 GB18030 字节序列

### GB18030 解码算法
1. **字节分析**: 检查字节是 ASCII 还是 GB18030 前导字节
2. **ASCII 处理**: ASCII 字节直接字符转换
3. **GB18030 处理**: 组合前导和尾随字节处理中文字符
4. **字符生成**: 使用映射表转换为 Unicode

### 错误处理策略
- **无效字节序列**: 检测并报告无效的 GB18030 序列
- **不完整序列**: 优雅地处理截断的字节序列
- **超出范围**: 验证字节范围并提供回退值
- **映射失败**: 对未映射字符使用默认值

## 🧪 测试覆盖

项目包含全面的测试用例，**代码覆盖率达85.61%**：
- ✅ 基本编解码功能测试
- ✅ 错误处理和边界情况测试
- ✅ Unicode 映射测试
- ✅ 字符分析和统计测试
- ✅ 性能和压力测试
- ✅ 复杂文本处理测试
- ✅ 批量操作测试
- ✅ 往返编码解码测试

### 测试统计
- **总测试数**: 118 个测试
- **通过率**: 100% (118/118 通过)
- **代码覆盖率**: 85.61% (113/132 行)
- **错误路径覆盖**: 全面的错误处理测试
- **边界条件覆盖**: 边界情况和限制测试

## 🚀 构建和运行

```bash
# 构建项目
moon build

# 运行测试
moon test

# 生成覆盖率报告
moon coverage report -f cobertura -o coverage.xml
```

## 📦 依赖

- `moonbitlang/core`: 提供基础数据结构支持
- `moonbitlang/core/immut/list`: 不可变列表实现，用于高效处理

## 📜 许可证

本项目采用 MIT 许可证。详情请参阅 LICENSE 文件。

## 📢 联系与支持

• MoonBit 社区: moonbit-community  
• GitHub Issues: 报告问题  

## 📝 更新日志

### v0.1.0
- ✅ 实现完整的 GB18030 编解码功能
- ✅ 支持多种输入/输出格式（字符串、数组、迭代器）
- ✅ 全面的 Unicode 到 GB18030 映射
- ✅ 健壮的错误处理和验证
- ✅ 字符分析和统计函数
- ✅ 高性能字节序列处理
- ✅ 全面的测试套件，覆盖率达85.61%
- ✅ 完整的文档和使用示例

## 🔍 GB18030 标准信息

GB18030 是官方的中文字符编码标准，支持：
- **ASCII 字符**: 0x00-0x7F
- **中文字符**: 0x4E00-0x9FFF（基本多语言平面）
- **扩展字符**: 各种 Unicode 范围
- **字节序列**: ASCII 1 字节，中文字符 2 字节

本库为 GB18030 标准提供完整支持，具有高效的编解码算法和全面的错误处理。

👋 如果您喜欢这个项目，请给它一个 ⭐！祝编码愉快！🚀 