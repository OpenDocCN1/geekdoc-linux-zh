• 准备sum_product[i]。在这个阶段，计算机将从内存中重新加载sum[i]和product[i].

第四个阶段是否存在进一步优化的空间呢？既然前面已经计算了sum[i]和product[i]，那么后面我们就不必再从内存中读取它们的值了。

答案是肯定的。

只是编译器本身不能在第三阶段确定前两个阶段的赋值没有被其他编译器覆盖。换而言之，因为编译器不能判断程序是否存在指向相同内存区域的指针——即“指针别名（aliasing）”，所以编译器不能确保该指针的内容未被改写。

C99标准中的限指针[1507, 6.7.3]（部分文献又称“严格别名”）的应生如此。程序员可以通过restrict修饰符向编译器承诺：被该关键字标记的指针是操作相关内存区域的唯一指针，没有其他指针指向该指针的内存区域。

用更严谨的语言来说，关键字“restrict”表示该指针是访问既定对象的唯一指针，其他指针都不会重复操作既定对象。从另一个角度来看，一旦指针被标记为受限指针，那么编译器就会确定既定对象只会会被指定的限限指针操作。

我们将为每个指针加上restrict修饰符：

```
void f2(int* restrict x, int* restrict y, int* restrict sum,
int* restrict product, int* * \
	restrict sum_product,
	int* restrict update_me, size_t s)
{
	for (int i=0; i<s; i++)
		sum[i]=x[i]+y[i];
		product[i]=x[i]*y[i];
		update_me[i]=i*123; // some dummy value
		sum_product[i]=sum[i]+product[i];
}

```

我们看到的结果如下。