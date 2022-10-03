---
title: 《 Metasploit 渗透测试指南》 第二章  Metasploit 基础
date: 2022-10-02 14:45:32
updated: 2022-10-02 14:45:32
categories: Metasploit 渗透测试指南
tags:
    - metasploit
    - penetration
    - security
    - hacker
description:
top_img: https://iili.io/iZZN49.jpg
cover: https://iili.io/iZZwE7.jpg
---

## 专业术语

### 渗透攻击(Expolit)

***渗透攻击***是由攻击者或渗透测试者利用一个系统、应用或服务中的安全漏洞，所进行的攻击行为。

### 攻击载荷(Payload)

***攻击载荷***是我们期望目标系统在被渗透攻击之后去执行的代码。

### shellcode

***shellcode*** 是在渗透攻击时作为攻击载荷运行的一组机器指令。

shellcode 通常以汇编语言编写。

在大多数情况下，目标系统执行了 shellcode 之后才会提供一个命令行 shell 或者 MeterPreter shell 。

### 模块(Module)

***模块***是指 Metasploit 框架中所使用的一段软件代码组件。

### 监听器(Listener)

***监听器***是 Metasploit 中用来等待网络连接的组件。

## Metasploit 用户接口

### MSF 终端

启动 msf 终端：

```shell
$ msfconsole

...

       =[ metasploit v6.2.19-dev                          ]
+ -- --=[ 2246 exploits - 1186 auxiliary - 399 post       ]
+ -- --=[ 951 payloads - 45 encoders - 11 nops            ]
+ -- --=[ 9 evasion                                       ]

Metasploit tip: View missing module options with show
missing
Metasploit Documentation: https://docs.metasploit.com/

msf6 >
```

### MSF 命令行

以被 msf 终端的 `-x` 选项替代。

### Armitage

Metasploit 图形化接口。

~~另外还有：[Metasploit Community Edition](https://www.offensive-security.com/metasploit-unleashed/msf-community-edition/)~~(已不在 Kali Linux 中提供)

## Metasploit 功能程序

### MSF 攻击载荷生成器

***MSF 攻击载荷生成器*** 允许你生成 shellcode、可执行代码和其他很多东西，也可以让它们在框架软件之外的渗透代码中进行使用。

`msfpayload` 已被弃用，由集成了攻击载荷生成和[编码](#msf-编码器)功能的 `msfvenom` 代替。

### MSF 编码器

编码器的作用：

+ shellcode 中可能存在空字符，在一些程序进行解析时，这些字符可能不认为是字符串的结束，从而使得代码在完整执行之前被阶段而终止执行。

  这些 `\x00` 和 `\xff` 字符会破坏你攻击载荷。

+ 编码可以避免 shellcode 被入侵检测系统(IDS)或杀毒软件识别。

编码功能被集成在了 `msfvenom` 功能程序中。

可用编码器：

```shell
$ msfvenom -l encoders

Framework Encoders [--encoder <value>]
======================================

    Name                          Rank       Description
    ----                          ----       -----------
    cmd/brace                     low        Bash Brace Expansion Command Encoder
    cmd/echo                      good       Echo Command Encoder
    cmd/generic_sh                manual     Generic Shell Variable Substitution Command Encoder
    cmd/ifs                       low        Bourne ${IFS} Substitution Command Encoder
    cmd/perl                      normal     Perl Command Encoder
    cmd/powershell_base64         excellent  Powershell Base64 Command Encoder
    cmd/printf_php_mq             manual     printf(1) via PHP magic_quotes Utility Command Encoder
    generic/eicar                 manual     The EICAR Encoder
    generic/none                  normal     The "none" Encoder
    mipsbe/byte_xori              normal     Byte XORi Encoder
    mipsbe/longxor                normal     XOR Encoder
    mipsle/byte_xori              normal     Byte XORi Encoder
    mipsle/longxor                normal     XOR Encoder
    php/base64                    great      PHP Base64 Encoder
    ppc/longxor                   normal     PPC LongXOR Encoder
    ppc/longxor_tag               normal     PPC LongXOR Encoder
    ruby/base64                   great      Ruby Base64 Encoder
    sparc/longxor_tag             normal     SPARC DWORD XOR Encoder
    x64/xor                       normal     XOR Encoder
    x64/xor_context               normal     Hostname-based Context Keyed Payload Encoder
    x64/xor_dynamic               normal     Dynamic key XOR Encoder
    x64/zutto_dekiru              manual     Zutto Dekiru
    x86/add_sub                   manual     Add/Sub Encoder
    x86/alpha_mixed               low        Alpha2 Alphanumeric Mixedcase Encoder
    x86/alpha_upper               low        Alpha2 Alphanumeric Uppercase Encoder
    x86/avoid_underscore_tolower  manual     Avoid underscore/tolower
    x86/avoid_utf8_tolower        manual     Avoid UTF8/tolower
    x86/bloxor                    manual     BloXor - A Metamorphic Block Based XOR Encoder
    x86/bmp_polyglot              manual     BMP Polyglot
    x86/call4_dword_xor           normal     Call+4 Dword XOR Encoder
    x86/context_cpuid             manual     CPUID-based Context Keyed Payload Encoder
    x86/context_stat              manual     stat(2)-based Context Keyed Payload Encoder
    x86/context_time              manual     time(2)-based Context Keyed Payload Encoder
    x86/countdown                 normal     Single-byte XOR Countdown Encoder
    x86/fnstenv_mov               normal     Variable-length Fnstenv/mov Dword XOR Encoder
    x86/jmp_call_additive         normal     Jump/Call XOR Additive Feedback Encoder
    x86/nonalpha                  low        Non-Alpha Encoder
    x86/nonupper                  low        Non-Upper Encoder
    x86/opt_sub                   manual     Sub Encoder (optimised)
    x86/service                   manual     Register Service
    x86/shikata_ga_nai            excellent  Polymorphic XOR Additive Feedback Encoder
    x86/single_static_bit         manual     Single Static Bit
    x86/unicode_mixed             manual     Alpha2 Alphanumeric Unicode Mixedcase Encoder
    x86/unicode_upper             manual     Alpha2 Alphanumeric Unicode Uppercase Encoder
    x86/xor_dynamic               normal     Dynamic key XOR Encoder
```

Name                          |Rank       |Description
----                          |----       |-----------
cmd/brace                     |low        |Bash Brace Expansion Command Encoder
cmd/echo                      |good       |Echo Command Encoder
cmd/generic_sh                |manual     |Generic Shell Variable Substitution Command Encoder
cmd/ifs                       |low        |Bourne ${IFS} Substitution Command Encoder
cmd/perl                      |normal     |Perl Command Encoder
cmd/powershell_base64         |excellent  |Powershell Base64 Command Encoder
cmd/printf_php_mq             |manual     |printf(1) via PHP magic_quotes Utility Command Encoder
generic/eicar                 |manual     |The EICAR Encoder
generic/none                  |normal     |The "none" Encoder
mipsbe/byte_xori              |normal     |Byte XORi Encoder
mipsbe/longxor                |normal     |XOR Encoder
mipsle/byte_xori              |normal     |Byte XORi Encoder
mipsle/longxor                |normal     |XOR Encoder
php/base64                    |great      |PHP Base64 Encoder
ppc/longxor                   |normal     |PPC LongXOR Encoder
ppc/longxor_tag               |normal     |PPC LongXOR Encoder
ruby/base64                   |great      |Ruby Base64 Encoder
sparc/longxor_tag             |normal     |SPARC DWORD XOR Encoder
x64/xor                       |normal     |XOR Encoder
x64/xor_context               |normal     |Hostname-based Context Keyed Payload Encoder
x64/xor_dynamic               |normal     |Dynamic key XOR Encoder
x64/zutto_dekiru              |manual     |Zutto Dekiru
x86/add_sub                   |manual     |Add/Sub Encoder
x86/alpha_mixed               |low        |Alpha2 Alphanumeric Mixedcase Encoder
x86/alpha_upper               |low        |Alpha2 Alphanumeric Uppercase Encoder
x86/avoid_underscore_tolower  |manual     |Avoid underscore/tolower
x86/avoid_utf8_tolower        |manual     |Avoid UTF8/tolower
x86/bloxor                    |manual     |BloXor - A Metamorphic Block Based XOR Encoder
x86/bmp_polyglot              |manual     |BMP Polyglot
x86/call4_dword_xor           |normal     |Call+4 Dword XOR Encoder
x86/context_cpuid             |manual     |CPUID-based Context Keyed Payload Encoder
x86/context_stat              |manual     |stat(2)-based Context Keyed Payload Encoder
x86/context_time              |manual     |time(2)-based Context Keyed Payload Encoder
x86/countdown                 |normal     |Single-byte XOR Countdown Encoder
x86/fnstenv_mov               |normal     |Variable-length Fnstenv/mov Dword XOR Encoder
x86/jmp_call_additive         |normal     |Jump/Call XOR Additive Feedback Encoder
x86/nonalpha                  |low        |Non-Alpha Encoder
x86/nonupper                  |low        |Non-Upper Encoder
x86/opt_sub                   |manual     |Sub Encoder (optimised)
x86/service                   |manual     |Register Service
x86/shikata_ga_nai            |excellent  |Polymorphic XOR Additive Feedback Encoder
x86/single_static_bit         |manual     |Single Static Bit
x86/unicode_mixed             |manual     |Alpha2 Alphanumeric Unicode Mixedcase Encoder
x86/unicode_upper             |manual     |Alpha2 Alphanumeric Unicode Uppercase Encoder
x86/xor_dynamic               |normal     |Dynamic key XOR Encoder

### Nasm shell

Nasm_shell.rb 是一个你尝试了解汇编代码含义时的一个非常有用的手头工具。

```shell
$ /usr/share/metasploit-framework/tools/exploit/nasm_shell.rb
nasm > jmp esp
00000000  FFE4              jmp esp
nasm >
```
