```
IRQF_TRIGGER_RISING | IRQF_TRIGGER_FALLING,
"gpiosmod#button1", NULL);

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

ret = request_irq(button_irqs[1], button_isr,
    IRQF_TRIGGER_RISING | IRQF_TRIGGER_FALLING,
    "gpiosmod#button2", NULL);

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

fail3:
    gpio_free(buttons[1].gpio);

fail2:
    gpio_free(buttons[0].gpio);

fail1:
    gpio_free(leds[0].gpio);
#else
fail3:
```