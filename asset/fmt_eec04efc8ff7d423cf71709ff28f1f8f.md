
```c
#include <linux/spi/spi.h>
#include <linux/interrupt.h>
#include <linux/of_gpio.h>
#include <linux/of_irq.h>
#include <linux/iio/iio.h>
#include <linux/wait.h>
#include <linux/workqueue.h>

static char *HELLO_KEYS_NAME = "SW5";
static int gpio_nb;
static int irq;
static bool done;
static DECLARE_WAIT_QUEUE(hello_keys_wait);

struct ADC_data {
    struct work_struct *ADC_wq;
    struct work_struct work;
    struct spi_device *spi;
    uint8_t buffer[4];
    char name[8];
};

static irq_return_t hello_keys_isr(int irq, void *data)
{
    pr_info("interrupt received: %s\n", HELLO_KEYS_NAME);
    struct iio_dev *indio_dev = data;

    /* 恢复 ADC_data 以将任务推入工作队列 */
    struct ADC_data *job = iio_priv(indio_dev);
    queue_work(job->ADC_wq, &job->work);

    return IRQ_HANDLED;
}

static void ADC_trigger_int(struct work_struct *work_s)
{
    pr_info("ISR bottom done!");
    done = true;
    wake_up(&hello_keys_wait);
}

static const iio_chan_spec ltc2422_channel[] = {
    .type = IIO_VOLTAGE,
    .scan = 1,
    .output = 1,
    .channel = 0,
    .mask = BIT(0),
};

static int ltc2422_read_raw(struct iio_dev *indio_dev,
    const iio_chan_spec *chan, long m)
{
    int ret_val;
    struct ADC_data *st = iio_priv(indio_dev);

    pr_info("Press SW5 to start");

    switch (m) {
        case IIO_SCAN_RAW:
            ret_val = wait_event_interruptible(hello_keys_wait, done);
            if (ret_val) {
                pr_err("Failed to request interrupt");
                return ret_val;
            }
            done = false;
        default:
            break;
    }
    return 0;
}

static struct iio_info ltc2422_info = {
    .read_raw = ltc2422_read_raw,
};.static struct iio_device ltc2422_dev = {
    .name = "ltc2422",
    .info = &ltc2422_info,
    .channels = ltc2422_channel,
    .num_channels = 1,
};

static int ltc2422_probe(struct spi_device *spi)
{
    struct iio_dev *indio_dev;
    struct ADC_data *st;
    int ret_val;

    pr_info("probe function called");
    indio_dev = devm_iio_alloc(spi->dev, sizeof(*st));
    if (indio_dev == NULL)
        return -ENOMEM;

    st = iio_priv(indio_dev);
    spi_set_drvdata(spi, indio_dev);

    indio_dev->dev = spi->dev;
    indio_dev->name = "ltc2422";
    indio_dev->info = &ltc2422_info;
    indio_dev->channels = ltc2422_channel;
    indio_dev->num_channels = 1;

    gpio_nb = gpiod_get_number(spi->dev, "", 0);
    pr_info("GPIO: %d\n", gpio_nb);
    irq = gpiod_to_irq(spi->dev, 0);
    pr_info("IRQ: %d\n", irq);

    st->ADC_wq = alloc_workqueue("ADC_wq", 0, 0);
    INIT_WORK(&st->work, ADC_trigger_int);

    ret_val = devm_request_interrupt(indio_dev->dev, irq,
    hello_keys_isr, IRQ_SHARED | IRQ_RISING, HELLO_KEYS_NAME, indio_dev);

    if (ret_val) {
        pr_err("Failed to request interrupt %d, error %d\n", irq, ret_val);
        return ret_val;
    }
    ret_val = devm_iio_device_register(spi->dev, indio_dev);
    if (ret_val < 0)
        return ret_val;
    return 0;
}

static int ltc2422_remove(struct spi_device *spi)
{
    struct iio_dev *indio_dev = spi_get_drvdata(spi);
    struct ADC_data *st = iio_priv(indio_dev);
    destroy_workqueue(st->ADC_wq);
    return 0;
}

static struct spi_driver ltc2422_driver = {
    .name = "ltc2422",
    .owner = THIS_MODULE,
    .of_match_table = ltc2422_dt_ids,
    .probe = ltc2422_probe,
    .remove = ltc2422_remove,
    .id_table = ltc2422_id,
};

module_spi_driver(ltc2422_driver);

MODULE_AUTHOR("Alberto Liberal <aliberal@arroweurope.com>");
MODULE_DESCRIPTION("LTC2422 DUAL ADC with hardware triggering");
MODULE_LICENSE("GPL");
```
