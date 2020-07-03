---
title: dialogue-papers
date: 2020-07-03 13:45:22
tags:
---

# 概述

这里记录我阅读的一些论文的核心知识点

# Sequicity: Simplifying Task-oriented Dialogue Systems with Single Sequence-to-Sequence Architectures

> [github code](https://github.com/WING-NUS/sequicity)

## Abstract

- 提出了一个新颖的、整体的、可扩展的框架，基于单序列对序列(seq2seq)模型
- 可通过监督或强化学习进行优化
- 使用 belief span 来跟踪对话状态
- 提供了`two stage copynet`实例，能够实现很好的扩展性和伸缩性：能够很好的缩短训练时间和参数量

## Introduction

- belief span 在状态跟踪中非常关键，因为是可以跟踪对话流程中各种关键信息
- 为每个槽都定义了一个多分类器，用以决策到底是什么数据类型
- 实际上我们能够为动态的训练及更新对应的槽位分类器
- 实现了跨文本的belief span，