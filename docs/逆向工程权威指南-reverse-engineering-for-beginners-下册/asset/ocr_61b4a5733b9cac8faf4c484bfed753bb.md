# 第93章 安腾指令

就市场来说，安腾 (Itanium) 处理器几乎是失败产品。但是它的 Intel Itanium (IA64) 架构非常值得研究。乱序执行（OoE）CPU理念，侧重于CPU重新指令的片段和顺序，再把重组后的指令组分发到并行计算单位进行并行计算。而英特尔（Intel）架构架构的并行计算技术（Explicitly Parallel Instruction Code, EPIC），则主张让编译器在编译的早期阶段实现指令分组。

厂商推出了配合这种并行计算技术的编译器。不过，这些编译器因为异常复杂而引起了争议。

本章从Linux内核（3.2.0.4）摘取了部分IA64指令。这段程序用于实现加密机制。其源代码如下所示。

指令清单93.1 Linux kernel 3.2.0.4

```
#define TEA_ROUNDS             32
#define TEA_DELTA             0x9e3779b9

static void tea_encrypt(struct crypto_ctx *tfm, u8 *dst, u8 *src)
{
	u32 y, z, n, sum = 0;
	u32 k0, k1, k2, k3;
	struct_ctx *ctx = crypto_ctx(tfm);
	const _le32 *in = (const _le32 *)src;
	_le32 *out = (_le32 *)dst;

ny = le32_to_cpu(in[0]);
	z = le32_to_cpu(in[1]);

	k0 = ctx->KEY[0];
	k1 = ctx->KEY[1];
```