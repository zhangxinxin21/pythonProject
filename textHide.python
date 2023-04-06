# -*- coding: utf-8 -*-

def hide_message_in_text(text, message):
    # 将消息转换为二进制字符串
    binary_message = ''.join(format(ord(c), '08b') for c in message)

    # 将汉字编码转换为整数
    code_list = []
    for c in text:
        code = ord(c)
        code_list.append(code)

    # 隐藏消息
    i = 0
    for j in range(len(code_list)):
        if i >= len(binary_message):
            break
        code = code_list[j]
        if code < 128:  # 只考虑 ASCII 码
            continue
        code_str = '{:016b}'.format(code)  # 转换为 16 位二进制字符串
        new_code_str = code_str[:14] + binary_message[i:i+2] + code_str[14:]
        new_code = int(new_code_str, 2)
        code_list[j] = new_code
        i += 2

    # 将整数转换为汉字编码
    new_text = ''
    for code in code_list:
        new_text += chr(code)

    return new_text


def extract_message_from_text(text):
    binary_message = ''
    code_list = [ord(c) for c in text]
    for code in code_list:
        if code < 128:
            continue
        code_str = '{:016b}'.format(code)  # 转换为 16 位二进制字符串
        binary_message += code_str[14:16]

    message = ''
    for i in range(0, len(binary_message), 8):
        byte = binary_message[i:i+8]
        if not byte:
            break
        message += chr(int(byte, 2))

    return message


# 测试代码
text = '这是一个测试文本，用于演示信息隐藏的功能。'
message = '秘密'
new_text = hide_message_in_text(text, message)
print('嵌入消息后的文本：', new_text)
extracted_message = extract_message_from_text(new_text)
print('提取出的隐藏消息：', extracted_message)
