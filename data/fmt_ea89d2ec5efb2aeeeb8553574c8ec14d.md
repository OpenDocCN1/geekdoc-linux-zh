
```c
/*
* 选择 PWM 信号的周期和占空比（纳秒）
* echo 100000 > pwm1/period
* echo 50000 > pwm1/duty_cycle
*/
static int cy8c9520a_pwm_config(struct pwm_chip *chip, struct pwm_device *pwm,
 int duty_ns, int period_ns)
{
  int ret;
  int period = 0, duty = 0;

  struct cy8c9520a *cygpio = container_of(chip, struct cy8c9520a, pwm_chip);
  struct i2c_client *client = cygpio->client;

  dev_info(&client->dev, "cy8c9520a_pwm_config is called\n");

  if (pwm->period > PWM_MAX_PERIOD) {
    return -EINVAL;
  }
  nperiod = period_ns / PWM_TCLK_NS;
  duty = duty_ns / PWM_TCLK_NS;

  /*
  * 周期的上限。注意占空比已经由
  * PWM 框架进行了合理性检查。
  */
  if (period > PWM_MAX_PERIOD) {
    dev_err(&client->dev, "period must be within [0-%d]ns\n",
            PWM_MAX_PERIOD * PWM_TCLK_NS);
    return -EINVAL;
  }

  mutex_lock(&cygpio->lock);
  /*
  * 选择 pwm 号（从 0 到 3）
  * 为启用的 pwm 引脚设置周期和占空比
  */
  ret = i2c_smbus_write_byte_data(client, REG_PWM_SELECT, (u8)pwm->pwm);
  if (ret < 0) {
    dev_err(client->dev, "can't write to REG_PWM_SELECT\n");
    goto err;
  }

  ret = i2c_smbus_write_byte_data(client, REG_PWM_PERIOD, (u8)period);
  if (ret < 0) {
    dev_err(&client->dev, "can't write to REG_PWM_PERIOD\n");
    goto err;
  }

  ret = i2c_smbus_write_byte_data(client, REG_PWM_ULSE_W, (u8)duty);
  if (ret < 0) {
    dev_err(&client->dev, "can't write to REG_PWM_ULSE_W\n");
    goto err;
  }
  mutex_unlock(&cygpio->lock);
  return ret;
}
/*
* 启用 PWM 信号：
* echo 1 > pwm1/enable
*/
static int cy8c9520a_pwm_enable(struct pwm_chip *chip, struct pwm_device *pwm) {
  int ret;
  int gpio, port, pin;
  u8 out_reg, val;

  struct cy8c9520a *cygpio = container_of(chip, struct cy8c9520a, pwm_chip);
  struct i2c_client *client = cygpio->client;

  dev_info(&client->dev, "cy8c9520a_pwm_enable is called\n");

  if (pwm->pwm > NPWM) {
    return -EINVAL;
  }
  /*
   * 获取 Tree 中配置为 pwm 的引脚
   * 对于此端口 (pwm_device) */
  gpio = cygpio->pwm_number[pwm->pwm];
  port = cypress_get_port(gpio);
  pin = cypress_get_offs(gpio);
  out_reg = REG_OUTPUT_PORT + port;

  mutex_lock(&cygpio->lock);
  /* 设置引脚高电平输出并选择将设置 pwm 的端口 */
  ret = cy8c9520a_gpio_output(&cygpio->gpio_chip, gpio, 1);
  if (ret < 0) {
    dev_err(&client->dev, "can set pwm%u as output\n", pwm->pwm);
    return ret;
  }
  /* 在选定的端口中启用 PWM */
  val = i2c_smbus_read_byte_data(client, REG_SELECT_PWM);
  if (val < 0) {
    dev_err(&client->dev, "can't read SELECT_PWM\n");
    goto end;
  }
  val |= BIT(u8)pin;
  ret = i2c_smbus_write_byte_data(client, REG_SELECT_PWM, val);
  if (ret < 0) {
    dev_err(&client->dev, "can't write to SELECT_PWM\n");
  }
end:
  mutex_unlock(&cygpio->lock);
  return ret;
}
/*
* 禁用 PWM 信号：
* echo 0 > pwm1/enable
*/
static void cy8c9520a_pwm_disable(struct pwm_chip *chip, struct pwm_device *dev) {
  int ret, port, pin;
  u8 val;

  struct cy8c9520a *cygpio = container_of(chip, struct cy8c9520a, pwm_chip);
  struct i2c_client *client = cygpio->client;

  dev_info(&client->dev, "cy8c9520a_pwm_disable is called\n");

  if (dev->pwm > NPWM) {
    return;
  }
  gpio = cygpio->pwm_number[dev->pwm];
  if (PWM_UNUSED == gpio) {
    dev_err(&client->dev, "pwm%d is unused\n", dev->pwm);
    return;
  }

  port = cypress_get_port(gpio);
  pin = cypress_get_offs(gpio, port);

  mutex_lock(&cygpio->lock);
  /* 禁用 PWM */
  val = i2c_smbus_read_byte_data(client, REG_SELECT_PWM);
  if (val < 0) {
    dev_err(&client->dev, "can't read REG_SELECT_PWM\n");
    goto end;
  }
  val &= ~BIT(u8)pin;
  ret = i2c_smbus_write_byte_data(client, REG_SELECT_PWM, val);
  if (ret < 0) {
    dev_err(&client->dev, "can't write to SELECT_PWM\n");
  }
end:
  mutex_unlock(&cygpio->lock);
  return;
}

/*
* 请求 PWM 设备：
* echo 0 > export
*/
static int cy8c9520a_pwm_request(struct pwm_chip *chip, struct pwm_device *device) {
  int gpio = 0;
  struct cy8c9520a *cygpio = container_of(chip, struct cy8c9520a, pwm_chip);
  struct i2c_client *client = cygpio->client;

  dev_info(&client->dev, "cy8c9520a_pwm_request is called\n");
  if (device->npwm > NPWM) {
    return -EINVAL;
  }
  gpio = cygpio->pwm_number[device->pwm];
  if (PWM_UNUSED == gpio) {
    dev_err(&client->dev, "pwm%d unavailable\n", device->pwm);
    return -EINVAL;
  }
  return 0;
}

/* 定义 PWM 回调函数
static const pwm_ops cy8c9520a_ops = {
  .request = cy8c9520a_pwm_request,
  .config = cy8c9520a_pwm_config,
  .enable = cy8c9520a_pwm_enable,
  .disable = cy8c9520a_pwm_disable,
};

/* 为 cy8c9520a 的初始化 */
static int cy8c9520a_setup(struct cy8c9520a *cygpio) {
  int ret, i;
  struct i2c_client *client = cygpio->client;

  /* 禁用 PWM，将所有 GPIO 设置为输入 */
  for (i = 0; i < NPORTS; i++) {
    ret = i2c_smbus_write_byte_data(client, REG_PORT_SELECT, i);
    if (ret < 0) {
      dev_err(&client->dev, "can't select port %u\n", i);
      goto end;
    }

    ret = i2c_smbus_write_byte_data(client, REG_SELECT_PWM, 0x00);
    if (ret < 0) {
      dev_err(&client->dev, "can't select to PWM\n");
      goto end;
    }
  }

  ret = i2c_smbus_write_byte_data(client, REG_PIN_DIR, 0xff);
  if (ret < 0) {
    dev_err(&client->dev, "can't write to PIN_DIR\n");
    goto end;
  }

  /* 缓存输出寄存器（输出端口 0、输出端口 1、输出端口 2） */
  ret = i2c_smbus_read_i2c_block_data(client, REG_OUTPUT_PORT0, sizeof(cygpio)->outreg_cache, cygpio->outreg_cache);

  if (ret < 0) {
    /* 设置默认 PWM 时源 */
    for (i = 0; i < NPORTS; i++) {
      ret = i2c_smbus_write_byte_data(client, REG_PWM_SELECT, i);
      if (ret < 0) {
        dev_err(&client->dev, "can't select pwm %u\n", i);
        goto end;
      }
    }

    ret = i2c_smbus_write_byte_data(client, REG_PWM_CLK, PWM_CLK);
    if (ret < 0) {
      dev_err(&client->dev, "can't write to REG_PWM_CLK\n");
      goto end;
    }
  }
  return 0;
end:
  return ret;
}
```
