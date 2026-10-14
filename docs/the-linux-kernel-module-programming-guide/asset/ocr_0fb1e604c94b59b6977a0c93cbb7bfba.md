```
135 static const struct file_operations vinput_fops = {
136 #if LINUX_VERSION_CODE < KERNEL_VERSION(6, 4, 0)
137 .owner = THIS_MODULE,
138 #endif
139 .open = vinput_open,
140 .release = vinput_release,
141 .read = vinput_read,
142 .write = vinput_write,
143 };
145 static void vinput_unregister_vdevice(struct vinput *vinput)
146 {
147     input_unregister_device(vinput->input);
148     if (vinput->type->ops->kill)
149         vinput->type->ops->kill(vinput);
150 }
152 static void vinput_destroy_vdevice(struct vinput *vinput)
153 {
154     /* Remove from the list first */
155     spin_lock(&vinput_lock);
156     list_del(&vinput->list);
157     clear_bit(vinput->id, vinput_ids);
158     spin_unlock(&vinput_lock);
160     module_put(THIS_MODULE);
162     kfree(vinput);
163 }
165 static void vinput_release_dev(struct device *dev)
166 {
167     struct vinput *vinput = dev_to_vinput(dev);
168     int id = vinput->id;
170     vinput_destroy_vdevice(vinput);
172     pr_debug("released vinput/%d\n", id);
173 }
175 static struct vinput *vinput_alloc_vdevice(void)
176 {
177     int err;
178     struct vinput *vinput = kzalloc(sizeof(struct vinput), GFP_KERNEL);
180     if (!vinput) {
181         pr_err("vinput: Cannot allocate vinput input device\n");
182         return ERR_PTR(-ENOMEM);
183     }
185     try_module_get(THIS_MODULE);
187     spin_lock_init(&vinput->lock);
189     spin_lock(&vinput_lock);
190     vinput->id = find_first_zero_bit(vinput_ids, VINPUT_MINORS);
191     if (vinput->id >= VINPUT_MINORS) {
```