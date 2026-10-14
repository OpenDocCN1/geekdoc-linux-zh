```
125 |     else    goto fail3;
126 | #else
127 |     goto fail2;
128 | #endif
129 |   }
130 |
131 |     button_irqs[1] = ret;
132 |
133 |     pr_info("Successfully requested BUTTON2 IRQ # %d\n", button_irqs[1]);
134 |
135 |     ret = request_irq(button_irqs[1], button_irq,
136 |                     IRQF_TRIGGER_RISING | IRQF_TRIGGER_FALLING,
137 |                     "gpiosmod#button2", NULL);
138 |
139 |     if (ret) {
140 |         pr_err("Unable to request IRQ: %d\n", ret);
141 | #ifdef NO_GPIO_REQUEST_ARRAY
142 |         goto fail4;
143 | #else
144 |         goto fail3;
145 | #endif
146 |     }
147 |
148 |     return 0;
149 |
150 | /* cleanup what has been setup so far */
151 | #ifdef NO_GPIO_REQUEST_ARRAY
152 | fail4:
153 |     free_irq(button_irqs[0], NULL);
154 |
155 | fail3:
156 |     gpio_free(buttons[1].gpio);
157 |
158 | fail2:
159 |     gpio_free(buttons[0].gpio);
160 |
161 | fail1:
162 |     gpio_free(leds[0].gpio);
163 | #else
164 | fail3:
165 |     free_irq(button_irqs[0], NULL);
166 |
167 | fail2:
168 |     gpio_free_array(buttons, ARRAY_SIZE(leds));
169 |
170 | fail1:
171 |     gpio_free_array(leds, ARRAY_SIZE(leds));
172 | #endif
173 |
174 |     return ret;
175 | }
176 |
177 | static void __exit intrpt_exit(void)
178 | {
179 |     pr_info("%s\n", __func__);
180 |     /* free irqs */
```