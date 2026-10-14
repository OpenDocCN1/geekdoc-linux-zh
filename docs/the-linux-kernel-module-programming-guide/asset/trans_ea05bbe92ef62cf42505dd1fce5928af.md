

#endif
}

button_irqs[0] = ret;

pr_info("Successfully requested BUTTON1 IRQ # %d\n", button_irqs[0]);

ret = request_threaded_irq(button_irqs[0], button_top_half,
                        button_bottom_half,
                        IRQF_TRIGGER_RISING | IRQF_TRIGGER_FALLING,
                        "gpio mod#button1", &buttons[0]);

if (ret) {
    pr_err("Unable to request IRQ: %d\n", ret);
#ifdef NO_GPIO_REQUEST_ARRAY
    goto fail3;
#else
    goto fail2;
#endif
}

ret = gpio_to_irq(buttons[1].gpio);

if (ret < 0) {
    pr_err("Unable to request IRQ: %d\n", ret);
#ifdef NO_GPIO_REQUEST_ARRAY
    goto fail3;
#else
    goto fail2;
#endif
}

button_irqs[1] = ret;

pr_info("Successfully requested BUTTON2 IRQ # %d\n", button_irqs[1]);

ret = request_threaded_irq(button_irqs[1], button_top_half,
                        button_bottom_half,
                        IRQF_TRIGGER_RISING | IRQF_TRIGGER_FALLING,
                        "gpio mod#button2", &buttons[1]);

if (ret) {
    pr_err("Unable to request IRQ: %d\n", ret);
#ifdef NO_GPIO_REQUEST_ARRAY
    goto fail4;
#else
    goto fail3;
#endif
}

return 0;

/* cleanup what has been setup so far */
#ifdef NO_GPIO_REQUEST_ARRAY
fail4:
free_irq(button_irqs[0], NULL);
161 fail3:
162   gpio_free(buttons[1].gpio);
164 fail2:
165   gpio_free(buttons[0].gpio);
167 fail1:
168   gpio_free(leds[0].gpio);
169 #else
170 fail3:
171   free_irq(button_irqs[0], NULL);
173 fail2:
174   gpio_free_array(buttons, ARRAY_SIZE(leds));
176 fail1:
177   gpio_free_array(leds, ARRAY_SIZE(leds));
178 #endif
180   return ret;
181 }
183 static void __exit bottomhalf_exit(void)
184 {
185   pr_info("\n", __func__);
187   /* free irqs */
188   free_irq(button_irqs[0], NULL);
189   free_irq(button_irqs[1], NULL);
191   /* turn all LEDs off */
192 #ifdef NO_GPIO_REQUEST_ARRAY
193   gpio_set_value(leds[0].gpio, 0);
195 #else
196   int i;
197   for (i = 0; i < ARRAY_SIZE(leds); i++)
198     gpio_set_value(leds[i].gpio, 0);
199 #endif
201   /* unregister */
202 #ifdef NO_GPIO_REQUEST_ARRAY
203   gpio_free(leds[0].gpio);
204   gpio_free(buttons[0].gpio);
205   gpio_free(buttons[1].gpio);
207 #else
208   gpio_free_array(leds, ARRAY_SIZE(leds));
209   gpio_free_array(buttons, ARRAY_SIZE(buttons));
210 #endif
211 }
212 module_init(bottomhalf_init);
213 module_exit(bottomhalf_exit);
214 MODULE_LICENSE("GPL");
215 MODULE_DESCRIPTION("Interrupt with top and bottom half");

使用 `request_threaded_irq()` 注册了一个线程化 IRQ。该函数

与 `request_irq()` 相比仅多了一个额外参数——在独立线程中运行的底半部处理函数。在本例中它就是 `button_bottom_half()`。其他参数的使用与 `request_irq()` 相同。

两个处理函数的存在并非强制。如果其中一个不需要，则传递 `NULL` 即可。`NULL` 的顶半部处理程序意味着除了唤醒运行底半部处理程序的底半部服务线程外不采取任何操作。类似地，`NULL` 的底半部处理程序实际上等同于使用了 `request_irq()`。事实上，这就是 `request_irq()` 的实现方式。

请注意，同时向两个处理程序传递 `NULL` 被视为错误，将导致注册失败。

## 16 虚拟输入设备驱动

输入设备驱动是一个模块，它提供了一种通过事件与交互设备通信的方式。例如，键盘可以发送按下或释放事件来告诉内核我们想要做什么。输入设备驱动将使用 `input_allocate_device()` 分配一个新的输入结构并设置输入位域、设备 ID、版本等。之后，通过调用 `input_register_device()` 将其注册。

下面是一个示例，vinput，它是一个 API，可让虚拟输入驱动的开发变得简单。驱动程序需要导出一个 `vinput_device()`，其中包含虚拟设备名称和描述以下内容的 `vinput_ops` 结构：

- 初始化函数：init()
- 输入事件注入函数：send()
- 回读函数：read()

然后使用 `vinput_register_device()` 和 `vinput_unregister_device()` 将新设备添加到支持的虚拟输入设备列表中。

```
int init(struct vinput *);
```

此函数会传入一个已初始化并分配了 `struct input_dev` 的 `struct vinput`。`init()` 函数负责初始化输入设备的 capabilities 并注册它。

```
int send(struct vinput *, char *, int);
```

此函数将接收一个用户字符串进行解释，并使用 `input_report_XXX` 或 `input_event` 调用注入事件。字符串已从用户处复制。

```
int read(struct vinput *, char *, int);
```

