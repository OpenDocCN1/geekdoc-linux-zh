```
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
```

A threaded IRQ is registered using request_threaded_irq(). This function