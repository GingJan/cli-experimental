---
title: "提交 Bug 报告"
linkTitle: "提交 Bug 报告"
type: docs
weight: 10
description: >
    如何提交 Bug 并修复 Kustomize 的问题
---


[krusty package]: https://github.com/kubernetes-sigs/kustomize/tree/master/api/krusty
[reusable custom transformer test]: https://github.com/kubernetes-sigs/kustomize/tree/master/api/krusty/customconfigreusable_test.go

您可以根据需要提交 Issue，但如果您发现了有关 `kustomize build` 工作方式的问题，请务必提供以下信息以便我们定位问题：

* `kustomize version` 命令的输出结果,
* 输入内容（包括 `kustomization.yaml` 文件及其引用的所有相关文件），
* 您期望生成的 `YAML` 格式的内容。

## 如果您已安装了 `go` 环境

Kustomize 在 [krusty
package] 包中提供了一个简易的测试框架，用于指定 kustomization 文件的输入及您期望输出的内容。

你可以复制其中一个测试用例，例如复制这个[可复用自定义转换器测试用例]，并将其粘贴为 krusty 包中的一个新测试文件。

插入你想用的输入，然后运行它：

```
(cd api; go test -run TestReusableCustomTransformers ./krusty)
```

命令的输出会显示bug和缺失的功能。

Record this output in the test file in a call to
`AssertActualEqualsExpected`, per all the other tests
in the [krusty package].  This makes the test pass,
albeit with output demonstrating behavior you
presumably want to change.

Send the new test in a PR, along with commentary (in
the test) on what you'd prefer to see.

The person who fixes the bug then has a clear bug
reproduction and a test to modify when the bug is
fixed.

Any bug fix first requires a test demonstrating the bug
(so we have permanent regression coverage), so if the
_bug reporter_ does this, it saves time and avoids
misunderstandings.
