---
title: Legate Sparse论文总结报告
date: 2024-04-12 10:36:49
tags: 文献阅读
---

# Legate Sparse: Distributed Sparse Computing in Python

## 摘要

"Legate Sparse: Distributed Sparse Computing in Python" 是一篇介绍Legate Sparse系统的研究论文，该系统旨在透明地分布和加速基于SciPy的稀疏矩阵程序，并能够在CPU和GPU集群上执行。Legate Sparse与cuNumeric（一个分布式NumPy库）协同工作，使用静态和动态技术高效地组合稀疏和密集数组编程库，为分布式稀疏和密集数组计算提供统一的Python接口。研究表明，Legate Sparse在单GPU库（如CuPy）上具有竞争力，并在Summit超级计算机上达到1280个CPU核心和192个GPU的性能，同时提供idiomatic SciPy和NumPy的生产力优势。

## 引言

Python因其易用性和丰富的数值库生态系统而在数据科学、机器学习和科学计算中被广泛使用。特别是NumPy和SciPy库，它们分别用于密集和稀疏矩阵计算，是许多应用程序和框架的基础。然而，这些库的标准实现仅限于单个CPU节点，并且只有少数操作支持多线程。随着数据集大小和应用计算需求的增加，有必要利用超出单个CPU节点所能提供的更强大的资源。尽管最近的工作在密集数组编程系统方面取得了很大进展，但自动分布和加速基于SciPy的稀疏矩阵程序尚未实现。Legate Sparse的目标是开发一个系统，该系统能够在分布式机器上扩展未修改的SciPy Sparse程序，并与cuNumeric高效组合。

## 背景

本节提供了有关SciPy Sparse模块的背景信息，并讨论了与本研究相关的库组件。此外，还介绍了Legion运行时系统，Legate Sparse和cuNumeric都是建立在该系统之上的。cuNumeric是一个分布式和加速的NumPy替代品，它通过动态将NumPy API转换为Legion任务来实现。

## 稀疏数据表示

Legate Sparse使用Legion的区域（regions）来表示稀疏矩阵，这些区域被划分为子区域以进行并行处理。通过Legion的图像（image）分区操作，Legate Sparse能够表达稀疏矩阵的共分区，并实现类似于MPI的散布/聚集操作。

## 可组合并行化

Legate Sparse和cuNumeric通过将每个操作转换为一系列在分区区域上的任务启动来分布SciPy和NumPy程序。通过使用基于约束的并行化和动态运行时系统，Legate Sparse能够与cuNumeric在分布式层上高效组合。

## 内核实现

Legate Sparse的原型实现了SciPy Sparse API的35%，足以表达科学计算和机器学习中的复杂计算。实现这些API的方法包括使用DISTAL编译器生成代码、从现有的SciPy或CuPy实现中移植代码，以及手写代码。

## 评估

Legate Sparse在Summit超级计算机上的性能通过一系列SciPy程序进行了评估，这些程序涵盖了从微基准测试到完整应用程序的不同复杂性。Legate Sparse在CPU和GPU模式下的性能都得到了测试，并与仅支持CPU或GPU的系统进行了比较。

## 相关工作

本节讨论了分布式稀疏线性代数和张量代数库、加速和分布式NumPy的相关研究工作。

## 结论

Legate Sparse为分布和加速未修改的SciPy Sparse程序提供了一种解决方案，并与cuNumeric高效组合。Legate Sparse的开发解决了软件堆栈中的可组合性问题，并为开发高性能分布式库提供了一种模型。