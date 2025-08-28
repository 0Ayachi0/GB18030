# GB18030 Encoding Library for MoonBit

[![Build Status](https://img.shields.io/github/actions/workflow/status/0Ayachi0/GB18030/ci.yml)](https://github.com/0Ayachi0/GB18030/actions) [![codecov](https://codecov.io/gh/0Ayachi0/GB18030/branch/main/graph/badge.svg)](https://codecov.io/gh/0Ayachi0/GB18030)

[简体中文](README_zh_CN.md) | English

A comprehensive GB18030 encoding/decoding library implemented in MoonBit language, providing complete Unicode mapping and efficient byte sequence processing, supporting various Chinese character encoding standard requirements.

## 🚀 Key Features

• 🎯 **Core Encoding/Decoding** – Complete bidirectional GB18030 to Unicode conversion  
• 🔧 **Multiple Input Formats** – Support for strings, arrays, and iterators  
• 🚀 **Advanced Features** – Incremental encoding/decoding and batch processing  
• 📊 **Performance Optimization** – Efficient byte sequence processing and memory management  
• 🔄 **Error Handling** – Comprehensive error detection and recovery mechanisms  
• 🎨 **Flexible API** – Multiple encoding/decoding interfaces for different use cases  
• 📈 **Statistics & Analysis** – Character counting and Chinese character detection  
• 🔍 **Type Safety** – Complete error types with robust type system  
• 📦 **Batch Operations** – Efficient processing of large text data  
• 🧪 **Test Coverage** – Comprehensive test suite with 85.61% code coverage  
• 📚 **Complete Documentation** – Detailed usage examples and API reference  

## 📥 Installation

```bash
moon add 0Ayachi0/GB18030@0.1.0
```

## 🚀 Usage Guide

### 🔨 Basic Encoding/Decoding
Perform basic GB18030 encoding and decoding operations.

```moonbit
// Basic string encoding
let test_string = "Hello 你好 World 世界"
let encoded_result = encode_from_string(test_string)
match encoded_result {
    Ok(bytes) => {
        // Process encoded bytes
        let byte_count = bytes.length()
        // byte_count will be the total bytes needed
    }
    Err(_) => {
        // Handle encoding error
    }
}

// Basic byte decoding
let test_bytes = [72, 101, 108, 108, 111, 0xB0, 0xA1, 32, 87, 111, 114, 108, 100]  // "Hello中 World"
let decoded_result = decode_to_string(test_bytes)
match decoded_result {
    Ok(result_string) => {
        // Process decoded string
        let char_count = result_string.length()
    }
    Err(_) => {
        // Handle decoding error
    }
}
```

### 🎯 Advanced Encoding Operations
Use different input formats for encoding operations.

```moonbit
// Encode from character array
let char_array = ['H', 'e', 'l', 'l', 'o', ' ', '你', '好']
let encode_array_result = encode_from_array(char_array)
match encode_array_result {
    Ok(bytes) => {
        // Process encoded bytes
    }
    Err(_) => {
        // Handle error
    }
}

// Encode from iterator
let char_iter = char_array.iter()
let encode_iter_result = encode_from_iter(char_iter)
match encode_iter_result {
    Ok(bytes) => {
        // Process encoded bytes
    }
    Err(_) => {
        // Handle error
    }
}

// Get encoding length without actually encoding
let length = get_gb18030_length("Hello 你好")
// length will be the bytes needed for encoding
```

### 🔧 Advanced Decoding Operations
Use different output formats for decoding operations.

```moonbit
// Decode to character array
let decode_array_result = decode_to_array(test_bytes)
match decode_array_result {
    Ok(char_array) => {
        // Process character array
        let char_count = char_array.length()
    }
    Err(_) => {
        // Handle error
    }
}

// Decode to iterator
let decode_iter_result = decode_to_iter(test_bytes)
match decode_iter_result {
    Ok(iter) => {
        let count = iter.count()
        // Process iterator
    }
    Err(_) => {
        // Handle error
    }
}

// Get character count without full decoding
let char_count = decode(test_bytes)
match char_count {
    Ok(count) => {
        // count is the number of characters
    }
    Err(_) => {
        // Handle error
    }
}
```

### 🔄 Error Handling
Handle various encoding and decoding errors gracefully.

```moonbit
// Handle invalid byte sequences
let invalid_bytes = [0x81, 0x3F]  // Invalid GB18030 sequence
let decode_result = decode_to_string(invalid_bytes)
match decode_result {
    Ok(_) => {
        // Success case
    }
    Err(DecodeError::InvalidByteSequence) => {
        // Handle invalid byte sequence
    }
    Err(DecodeError::IncompleteByteSequence) => {
        // Handle incomplete byte sequence
    }
    Err(DecodeError::OutOfRange) => {
        // Handle out of range error
    }
}

// Handle encoding errors
let encode_result = encode_from_string("")
match encode_result {
    Ok(bytes) => {
        // Success case
    }
    Err(EncodeError::InvalidCharacter) => {
        // Handle invalid character
    }
    Err(EncodeError::UnsupportedEncoding) => {
        // Handle unsupported encoding
    }
}
```

### 📈 Character Analysis and Statistics
Analyze text content and get statistical information.

```moonbit
// Check if string contains Chinese characters
let has_chinese = contains_chinese("Hello 你好 World")
// has_chinese will be true

// Count ASCII characters
let ascii_count = count_ascii_chars("Hello 你好 World 123")
// ascii_count will be 18 (including spaces and numbers)

// Count Chinese characters
let chinese_count = count_chinese_chars("Hello 你好 World 世界")
// chinese_count will be 4

// Validate GB18030 byte sequence
let is_valid = is_valid_gb18030(test_bytes)
// is_valid will be true for valid sequences
```

### 🎨 Unicode Mapping
Handle Unicode to GB18030 mapping.

```moonbit
// Convert Unicode to GB18030
let unicode_char = 0x4E00  // "一" character
let gb_code = unicode_to_gb18030(unicode_char)
// gb_code will be 0xB0A1

// Convert GB18030 to Unicode
let gb18030_code = 0xB0A1
let unicode = gb18030_to_unicode(gb18030_code)
// unicode will be 0x4E00

// Handle out-of-range mapping
let invalid_unicode = 0x10FFFF  // Maximum Unicode value
let result = unicode_to_gb18030(invalid_unicode)
// result will be 0x3F3F (default value)
```

### 🏗️ Complex Text Processing
Handle complex text processing scenarios.

```moonbit
// Process large text with mixed content
let large_text = "This is a very long text that contains many characters and should be handled properly by the encoding system. 这是一个很长的文本，包含很多字符，应该被编码系统正确处理。"

let encode_result = encode_from_string(large_text)
match encode_result {
    Ok(bytes) => {
        // Process large encoded data
        let total_bytes = bytes.length()
        
        // Decode back for verification
        let decode_result = decode_to_string(bytes)
        match decode_result {
            Ok(decoded_text) => {
                // Verify encoding/decoding integrity
                let is_same = decoded_text == large_text
            }
            Err(_) => {
                // Handle decoding error
            }
        }
    }
    Err(_) => {
        // Handle encoding error
    }
}

// Batch process multiple strings
let text_list = ["Hello", "你好", "World", "世界", "123", "!@#"]
let mut all_bytes = []

for text in text_list {
    let encode_result = encode_from_string(text)
    match encode_result {
        Ok(bytes) => {
            all_bytes = all_bytes + bytes
        }
        Err(_) => {
            // Handle error for this text
        }
    }
}
```

## 📋 Data Structures

### Error Types
```moonbit
enum DecodeError {
    InvalidByteSequence,    // Invalid GB18030 byte sequence
    IncompleteByteSequence, // Incomplete byte sequence
    OutOfRange             // Byte sequence out of valid range
}

enum EncodeError {
    InvalidCharacter,      // Invalid encoding character
    UnsupportedEncoding    // Unsupported encoding format
}
```

### Core Functions
```moonbit
// Encoding functions
encode_from_string(s: String) -> Result[Array[Int], EncodeError]
encode_from_array(chars: Array[Char]) -> Result[Array[Int], EncodeError]
encode_from_iter(chars: Iter[Char]) -> Result[Array[Int], EncodeError]

// Decoding functions
decode_to_string(bytes: Array[Int]) -> Result[String, DecodeError]
decode_to_array(bytes: Array[Int]) -> Result[Array[Char], DecodeError]
decode_to_iter(bytes: Array[Int]) -> Result[Iter[Char], DecodeError]
decode(bytes: Array[Int]) -> Result[Int, DecodeError]

// Utility functions
get_gb18030_length(s: String) -> Int
contains_chinese(s: String) -> Bool
count_ascii_chars(s: String) -> Int
count_chinese_chars(s: String) -> Int
is_valid_gb18030(bytes: Array[Int]) -> Bool

// Mapping functions
unicode_to_gb18030(unicode: Int) -> Int
gb18030_to_unicode(gb_code: Int) -> Int
```

## 📊 Complete API Reference

### Core Encoding/Decoding
- `encode_from_string(s)` - Encode string to GB18030 bytes
- `encode_from_array(chars)` - Encode character array to GB18030 bytes
- `encode_from_iter(chars)` - Encode character iterator to GB18030 bytes
- `decode_to_string(bytes)` - Decode GB18030 bytes to string
- `decode_to_array(bytes)` - Decode GB18030 bytes to character array
- `decode_to_iter(bytes)` - Decode GB18030 bytes to character iterator
- `decode(bytes)` - Get character count from GB18030 bytes

### Utility Functions
- `get_gb18030_length(s)` - Get encoding length of string
- `contains_chinese(s)` - Check if string contains Chinese characters
- `count_ascii_chars(s)` - Count ASCII characters in string
- `count_chinese_chars(s)` - Count Chinese characters in string
- `is_valid_gb18030(bytes)` - Validate GB18030 byte sequence

### Mapping Functions
- `unicode_to_gb18030(unicode)` - Convert Unicode to GB18030 code
- `gb18030_to_unicode(gb_code)` - Convert GB18030 code to Unicode

### Helper Functions
- `is_ascii(byte)` - Check if byte is ASCII
- `is_gb18030_lead(byte)` - Check if byte is GB18030 lead byte
- `is_gb18030_trail(byte)` - Check if byte is GB18030 trail byte

## 📈 Performance Characteristics

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
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

## 🏗️ Algorithm Details

### GB18030 Encoding Algorithm
1. **Character Analysis**: Check if character is ASCII or Chinese
2. **ASCII Processing**: Direct byte conversion for ASCII characters
3. **Chinese Processing**: Use mapping table for Chinese characters
4. **Byte Sequence Generation**: Generate correct GB18030 byte sequences

### GB18030 Decoding Algorithm
1. **Byte Analysis**: Check if byte is ASCII or GB18030 lead byte
2. **ASCII Processing**: Direct character conversion for ASCII bytes
3. **GB18030 Processing**: Combine lead and trail bytes for Chinese characters
4. **Character Generation**: Use mapping table to convert to Unicode

### Error Handling Strategy
- **Invalid Byte Sequences**: Detect and report invalid GB18030 sequences
- **Incomplete Sequences**: Gracefully handle truncated byte sequences
- **Out of Range**: Validate byte ranges and provide fallback values
- **Mapping Failures**: Use default values for unmapped characters

## 🧪 Test Coverage

Project includes comprehensive test cases with **85.61% code coverage**:
- ✅ Basic encoding/decoding functionality tests
- ✅ Error handling and edge case tests
- ✅ Unicode mapping tests
- ✅ Character analysis and statistics tests
- ✅ Performance and stress tests
- ✅ Complex text processing tests
- ✅ Batch operation tests
- ✅ Round-trip encoding/decoding tests

### Test Statistics
- **Total Tests**: 118 tests
- **Pass Rate**: 100% (118/118 passed)
- **Code Coverage**: 85.61% (113/132 lines)
- **Error Path Coverage**: Comprehensive error handling tests
- **Boundary Condition Coverage**: Edge cases and limit tests

## 🚀 Build and Run

```bash
# Build the project
moon build

# Run tests
moon test

# Generate coverage report
moon coverage report -f cobertura -o coverage.xml
```

## 📦 Dependencies

- `moonbitlang/core`: Provides basic data structure support
- `moonbitlang/core/immut/list`: Immutable list implementation for efficient processing

## 📜 License

This project is licensed under the MIT License. See the LICENSE file for details.

## 📢 Contact & Support

• MoonBit Community: moonbit-community  
• GitHub Issues: Report issues  

## 📝 Changelog

### v0.1.0
- ✅ Implemented complete GB18030 encoding/decoding functionality
- ✅ Support for multiple input/output formats (string, array, iterator)
- ✅ Comprehensive Unicode to GB18030 mapping
- ✅ Robust error handling and validation
- ✅ Character analysis and statistics functions
- ✅ High-performance byte sequence processing
- ✅ Comprehensive test suite with 85.61% coverage
- ✅ Complete documentation and usage examples

## 🔍 GB18030 Standard Information

GB18030 is the official Chinese character encoding standard, supporting:
- **ASCII Characters**: 0x00-0x7F
- **Chinese Characters**: 0x4E00-0x9FFF (Basic Multilingual Plane)
- **Extended Characters**: Various Unicode ranges
- **Byte Sequences**: ASCII 1 byte, Chinese characters 2 bytes

This library provides complete support for the GB18030 standard with efficient encoding/decoding algorithms and comprehensive error handling.

👋 If you like this project, please give it a ⭐! Happy coding! 🚀 